<template>
  <div>
    <p v-if="clicked" >{{ text }}</p>
    <button v-else class="btn" @click="handler">押してー</button>
  </div>
</template>

<script>
export default {
  name: 'Maker',
  props: ['text', 'clicked', 'handler']
}
</script>

<style scoped>
p {
  font-size: 40px;
}
.btn {
  margin-top: 40px;
}
</style>
