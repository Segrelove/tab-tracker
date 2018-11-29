<template>
  <v-layout align-center justify-center column fill-height>
      <v-flex offset-xs>
        <div class="white elevation-10">
          <v-toolbar flat dense class="cyan" dark>
            <v-toolbar-title>Register</v-toolbar-title>
          </v-toolbar>

          <div class="pl-4 pr-4 pt-2 pb-2">
            <v-text-field type="email" name="email"
            v-model="email"
            autocomplete="off"
            placeholder="Email"/><br>
            <v-text-field type="password" name="password"
            v-model="password"
            autocomplete="new-password"
            placeholder="Password"/><br>
            <div class="error" v-html="error"/>
            <v-btn @click="register" class="cyan" dark>Register</v-btn>
          </div>
        </div>
      </v-flex>
  </v-layout>
</template>

<script>
/* eslint-disable */
import AuthenticationService from '@/services/AuthenticationService'
export default {
  data () {
    return {
    email: '',
    password: '',
    error: null
    }
  },
  methods: {
    async register () {
      try {
        const response = await AuthenticationService.register({
          email: this.email,
          password: this.password
        })
      } catch (error) {
        this.error = error.response.data.error
      }
    }
  }
}
</script>

<style scoped>
.error {
  color: red;
}
</style>
