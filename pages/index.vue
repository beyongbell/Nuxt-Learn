<template>
  <div>
    <h1>{{ message }}</h1>
    <span :title="message"> Test Test </span>
  </div>
</template>

<script>
export default {
  data() {
    return {
      message: 'Hello Vue',
    }
  },
}
</script>

<style></style>
