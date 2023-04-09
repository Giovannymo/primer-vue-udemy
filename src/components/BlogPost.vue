<script setup>

defineProps({
  title: String,
  id: Number,
  body: {
    type: String,
    default: 'Sin Descripcion.'
  },
});


const emit = defineEmits(['selectPostFavorito']);
</script>

<template>
<div class="card">
  <div class="card-body">
    <h2 class="card-title">{{title}}</h2>
    <h6 class="card-subtitle text-muted">{{ id }} </h6>
    <p class="card-text">{{body}}</p>
    <button class="btn btn-outline-primary" @click="emit('selectPostFavorito', title)">Favorito</button>
  </div>
</div>
</template>

<style>
</style>