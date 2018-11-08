<template>
<v-layout>
  <v-flex xs6 offset-xs3>
    <div class="white elevation-2">
      <v-toolbar flat dense class="cyan">
        <v-toolbar-title>Register</v-toolbar-title>
      </v-toolbar>
      <v-form v-model="valid">
        <v-text-field 
          v-model="email"
          :rules="emailRules"
          label="Email"
          required
        ></v-text-field>
        <v-text-field 
          v-model="password"
          :rules="passwordRules"
          type="password"
          label="Password"
          required
        ></v-text-field>
        <div class="error" v-html="error" />
        <v-btn class="cyan" @click="register">Register</v-btn>
      </v-form>
        <!-- <v-input type="text" name="email" v-model="email" placeholder ="email"/>
        <v-input type="password" name="password" v-model="password" placeholder ="password"/> -->
    </div>
  </v-flex>
</v-layout>

</template>

<script>
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
      try{
        await AuthenticationService.register({
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

</style>
