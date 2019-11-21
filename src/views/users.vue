<template>
  <div>
    <h1>users</h1>
    <ul>
      <li v-for="user in users" :key="user.id">
        <router-link :to="'/user/'+user.id">{{user.name}}</router-link>
      </li>
    </ul>
  </div>
</template>
<script>
export default {
  data() {
    return {
      users: []
    };
  },
  async mounted() {
    this.users = await fetch("https://jsonplaceholder.typicode.com/users").then(
      res => res.json()
    );
  }
};
</script>
