<template>
  <div class="profile-header">
    <div class="profile-card">
      <div class="profile-left">
        <img class="avatar" src="@/assets/Avatar.png" alt="Avatar" />
      </div>
      <div class="profile-info">
        <h2 class="username">John Doe</h2>
        <p class="status">Last online: 2 days ago</p>
      </div>
      <div class="profile-actions">
        <button class="btn message-btn">
          <i class="icon">📨</i> Send Message
        </button>
        <button class="btn add-friend-btn">
          <i class="icon">➕</i> Add Friend
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Avatar_section",
};
</script>

<style scoped>
/* Full screen width header */
.profile-header {
  width: 100%;
  background-color: #2fc0df;
  padding: 20px 0;
  display: flex;
  justify-content: center; /* Align inner card to the right */
overflow: visible; /* Allow child to overflow */
height: 80px;

}

/* Inner profile card */
.profile-card {
  display: flex;
  align-items: flex-start;
  background-color: #2fc0df;
  color: white;
  border-radius: 6px;
  padding: 20px;
  margin-right: 20%; /* 👈 push it in from the right */
  width: fit-content;
  padding-top: 30px;

}

.avatar {
  width: 100px;
  height: 100px;
  border-radius: 8px;
  object-fit: cover;
  margin-right: 20px;
}

.profile-info {
  flex-grow: 1;
}

.username {
  margin: 0;
  font-size: 24px;
  font-weight: bold;
}

.status {
  margin-top: 5px;
  font-size: 14px;
  color: #e0f7fa;
}

.profile-actions {
  display: flex;
  gap: 10px;
  margin-left: 20px;
  overflow: visible;
  padding-top: 10px;
}

.btn {
  width: 140px; /* or min-width: 140px; */
  border: none;
  padding: 10px 12px;
  border-radius: 3px;
  cursor: pointer;
  font-weight: 300;
  display: flex;
  align-items: center;
  gap: 5px;
  transition: background 0.2s;
}

.btn:hover {

  outline: solid white 1px; /* custom solid border outline */
  outline-offset: 1px;
}

.message-btn {
  background-color: white;
  color: #2fc0df;
}
.add-friend-btn{
background-color: #2fc0df;
  color: white;
  outline: white solid 1px;
}
.message-btn:hover {
  background-color: #2fc0df;

    color: white; /* 👈 Change text color on hover */
  outline: white solid 1px;
}
.add-friend-btn:hover {
  background-color: white;
  color: #2fc0df; /* 👈 Change text color on hover */

}
</style>
