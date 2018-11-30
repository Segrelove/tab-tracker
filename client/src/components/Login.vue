<template>
  <v-layout align-center justify-center column fill-height>
      <v-flex offset-xs>
        <panel title="Login">
          <v-text-field type="email" name="email"
          v-model="email"
          placeholder="Email"/><br>
          <v-text-field type="password" name="password"
          v-model="password"
          placeholder="Password"/><br>
          <div class="error" v-html="error"/>
          <v-btn @click="login  " class="cyan" dark>login</v-btn>
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
    async login () {
      try {
        const response = await AuthenticationService.login({
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
  components :{
    Panel
  }
}
</script>

<style scoped>
.error {
  color: red;
}
</style>
