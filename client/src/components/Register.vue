<template>
  <v-layout align-center justify-center column fill-height>
    <v-flex offset-xs>
      <panel title="Register">
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
      </panel>
      </v-flex>
  </v-layout>
</template>

<script>
/* eslint-disable */
import AuthenticationService from '@/services/AuthenticationService'
import Panel from '@/components/Panel'

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
        this.$store.dispatch('setToken', response.data.token)
        this.$store.dispatch('setUser', response.data.user)
      } catch (error) {
        this.error = error.response.data.error
      }
    }
  },
  components: {
    Panel
  }
}
</script>

<style scoped>
.error {
  color: red;
}
</style>
