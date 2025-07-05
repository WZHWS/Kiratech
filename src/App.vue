
<template>
  <div class="container mx-auto p-4">
    <Header_section />
    <Avatar_section />
    <UserList />
  </div>
</template>

<script>
import Header_section from './components/Header.vue';
import Avatar_section from './components/Avatar.vue';
import UserList from './components/UserList.vue';

export default {
  components: {
    Header_section,
    Avatar_section,
    UserList
  }
};
</script>

<style scoped>
/* Optional: Global styles */
</style>
