<template>
  <v-toolbar fixed class="cyan" dark>
    <v-toolbar-title class="mr-4">
      <span class="home" @click="navigateTo({name: 'root'})">TabTracker</span>
    </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn flat dark @click="navigateTo({name: 'login'})">Log in
      </v-btn>
        <v-btn flat dark @click="navigateTo({name: 'Register'})">Sign Up
        </v-btn>
  </v-toolbar>
</template>

<script>
/* eslint-disable */
export default {
  methods: {
    navigateTo (route) {
      this.$router.push(route)
    }
  }

}
</script>

<style scoped>
.home {
  cursor: pointer;
}

.home:hover {
  color: #0f609e;
}

</style>
