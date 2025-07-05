<template>
  <div class="header-container">
    <!-- Left Section: Logo -->
    <div class="header-logo">
      <img src="@/assets/logo.png" alt="KIRATECH" />
    </div>

    <!-- Right Section: Icons -->
    <div class="header-right">
      <span class="icon" title="Notifications">
        <i class="fas fa-bell"></i>
      </span>
      <span class="icon" title="Settings">
        <i class="fas fa-cogs"></i>
      </span>
      <span class="icon" title="Logout">
        <i class="fas fa-sign-out-alt"></i>
      </span>
    </div>
  </div>
</template>

<script>
export default {
  name: "UserHeader",
};
</script>

<style scoped>
.header-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: white;
  padding: 1rem 2rem;
  border-bottom: 1px solid #e5e7eb;
  width: 50%;
    margin-left: 20%; /* 👈 shift icons a bit inward */

}

.header-logo {
  display: flex;
  align-items: center;
}

.header-logo img {
  height: 40px;
}

.header-right {
  display: flex;
  align-items: center;
  gap: 20px;
  margin-right: 5%; /* 👈 shift icons a bit inward */
}

.icon i {
  font-size: 1.25rem;
  color: #333;
  transition: color 0.2s;
}

.icon:hover i {
  color: #2fc0df;
  cursor: pointer;
}
</style>
