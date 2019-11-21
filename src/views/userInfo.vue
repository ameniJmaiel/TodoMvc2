<template>
  <div>
    <h1>user Info</h1>
    <h1 v-if="user">{{user.name}}</h1>
    <h1 v-if="user">{{user.email}}</h1>
    <h1 v-if="user">{{user.phone}}</h1>
    <h1 v-if="user">{{user.address.city}}</h1>
  </div>
</template>
<script>
export default {
  data() {
    return {
      user: null
    };
  },

  async mounted() {
    this.user = await fetch(
      "https://jsonplaceholder.typicode.com/users/" + this.$route.params.id
    ).then(res => res.json());
  }
};
</script>