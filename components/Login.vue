<template>
  <div>
    <input v-model="username" type="text" name="username" />
    <input v-model="password" type="password" name="password" />
    <br />
    <button @click="handleLoginClicked()">Login</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      username: '',
      password: '',
    }
  },
  methods: {
    handleLoginClicked() {
      this.$emit('login-submit', this.username, this.password)
    },
  },
}
</script>

<style></style>
