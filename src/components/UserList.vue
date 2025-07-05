<template>
  <div class="user-list-wrapper">
    <div class="max-width">
      <!-- Search Box -->
      <div class="search-container">
        <input
          v-model="searchQuery"
          type="text"
          placeholder="Search users..."
          class="search-input"
        />
      </div>

      <!-- Table Header -->
      <div class="table-header">
        <div>Date</div>
        <div>Name</div>
        <div>Gender</div>
        <div>Country</div>
        <div>Email</div>
      </div>

      <!-- User Rows -->
      <div class="user-rows-container">
        <div
          v-for="user in filteredUsers"
          :key="user.email"
          class="user-row"
          @click="openUserDetails(user)"
        >
          <div class="gray-text">{{ formatDate(user.dob.date) }}</div>
          <div
            :class="[
              'name-cell',
              selectedUser && selectedUser.email === user.email
                ? 'selected-name'
                : ''
            ]"
          >
            {{ user.name.first }} {{ user.name.last }}
          </div>
          <div class="gray-text">{{ capitalize(user.gender) }}</div>
          <div class="black-text">{{ user.location.country }}</div>
          <div class="gray-text email">{{ user.email }}</div>
        </div>
      </div>

      <!-- Refresh Button -->
      <div class="refresh-wrapper">
        <button @click="fetchUsers" class="refresh-button">
          <i class="fas fa-sync-alt"></i> Refresh
        </button>
      </div>
    </div>

    <!-- MODAL -->
    <div v-if="selectedUser" class="modal-overlay" @click.self="closeModal">
      <div class="modal-content">
        <div class="modal-header">
          <h3>{{ selectedUser.name.first }} {{ selectedUser.name.last }}</h3>
          <button @click="closeModal" class="close-button">&times;</button>
        </div>
        <div class="modal-body">
          <p>Date: {{ formatDate(selectedUser.dob.date) }}</p>
          <p>Status: Inactive</p>
          <p>Country: {{ selectedUser.location.country }}</p>
          <p>Email: {{ selectedUser.email }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "UserList",
  data() {
    return {
      users: [],
      selectedUser: null,
      searchQuery: "", // search input
    };
  },
  computed: {
    filteredUsers() {
      if (!this.searchQuery) return this.users;
      const query = this.searchQuery.toLowerCase();
      return this.users.filter(user =>
        (user.name.first + " " + user.name.last).toLowerCase().includes(query) ||
        user.email.toLowerCase().includes(query) ||
        user.location.country.toLowerCase().includes(query)
      );
    },
  },
  methods: {
    async fetchUsers() {
      try {
        const response = await axios.get("https://randomuser.me/api/?results=7");
        this.users = response.data.results;
      } catch (error) {
        console.error("Error fetching users:", error);
      }
    },
    openUserDetails(user) {
      this.selectedUser = user;
    },
    closeModal() {
      this.selectedUser = null;
    },
    formatDate(date) {
      const d = new Date(date);
      const day = String(d.getDate()).padStart(2, "0");
      const month = d.toLocaleString("en-US", { month: "short" });
      const year = d.getFullYear();
      return `${day} ${month} ${year}`;
    },
    capitalize(word) {
      if (!word) return "";
      return word.charAt(0).toUpperCase() + word.slice(1).toLowerCase();
    },
  },
  created() {
    this.fetchUsers();
  },
};
</script>

<style scoped>
/* page layout */
.user-list-wrapper {
  background-color: white;
  min-height: 100vh;
  padding: 2rem 1rem;
  margin-top: 50px;
  width: 50%;
  margin-left: 20%;
}
.max-width {
  max-width: 1000px;
  margin: 0 auto;
}

/* search */
.search-container {
  display: flex;
  justify-content: center;
  margin-bottom: 1rem;
}
.search-input {
  width: 50%;
  max-width: 400px;
  padding: 0.5rem 1rem;
  border: 1px solid #ddd;
  border-radius: 4px;
  font-size: 0.9rem;
}

/* table header */
.table-header {
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  background-color: white;
  color: gray;
  font-weight: 600;
  font-size: 0.75rem;
  padding: 0.75rem 1rem;
}

/* user rows */
.user-rows-container {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  margin-top: 1rem;
}
.user-row {
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  background-color: #ffffff;
  padding: 1rem;
  border-radius: 0.5rem;
  box-shadow: 0 1px 4px rgba(0,0,0,0.1);
  font-size: 0.875rem;
  cursor: pointer;
  transition: background-color 0.3s, box-shadow 0.3s;
}
.user-row:hover {
  background-color: #f0faff;
  box-shadow: 0 4px 8px rgba(0,0,0,0.15);
}
.name-cell {
  color: black;
  font-weight: 300;
  transition: color 0.3s;
}
.user-row:hover .name-cell {
  color: #2fc0df;
}
.selected-name {
  color: #2fc0df !important;
  font-weight: 300; /* stays normal weight */
}

.gray-text {
  color: #6b7280;
}
.black-text {
  color: black;
}
.email {
  word-break: break-word;
}

/* refresh button */
.refresh-wrapper {
  display: flex;
  justify-content: center;
  margin-top: 2rem;
}
.refresh-button {
  background-color: #2fc0df;
  color: white;
  padding: 0.5rem 1.5rem;
  border-radius: 0.375rem;
  transition: background-color 0.3s;
  font-size: 0.875rem;
  border: none;
  display: flex;
  align-items: center;
  gap: 0.5rem;
}
.refresh-button:hover {
  background-color: #28a6c2;
}

/* modal */
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0,0,0,0.5);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 10;
}
.modal-content {
  background: white;
  padding: 1.5rem;
  border-radius: 0.5rem;
  width: 25%;
  box-shadow: 0 4px 8px rgba(0,0,0,0.2);
  position: relative;
}
.modal-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-weight: bold;
  font-size: 1.1rem;
  margin-bottom: 1rem;
}
.close-button {
  background: transparent;
  color: grey;
  border: none;
  font-size: 1.2rem;
  cursor: pointer;
}
.modal-body p {
width: 50%;
  margin: 0.5rem 0;
  font-size: 0.9rem;
}
</style>
