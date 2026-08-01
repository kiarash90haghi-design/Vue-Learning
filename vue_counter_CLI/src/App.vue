<script setup lang="ts">
    import { ref } from 'vue';

    let counter = ref(0)


</script>

<template>
  <h1 id="heading">Counter is: {{ counter }}</h1>

  <button id="increment" @click="counter++">+</button>
  <button id="decrement" @click="counter--">-</button>
</template>

<style scoped>

</style>
