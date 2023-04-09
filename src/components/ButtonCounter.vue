<script setup>
import {ref, computed} from 'vue';

const counter = ref(0);
const increment = () =>{
  return counter.value++;
}

</script>

<template>

  <button class="btn btn-primary me-2 p-2" @click="increment">{{counter}}</button>
</template>

<style>
  .btn{
    width: 200px;
  }

</style>