<script setup> //自帶setup及return
  import { ref } from 'vue';
  
  const num = ref(2);
  function clickMe(){
    num.value++
  }
</script>

<template>
  <div>
    {{ num }}
    <button type="button" v-on:click="clickMe">點擊</button>
  </div>
</template>

<style scoped>

</style>
