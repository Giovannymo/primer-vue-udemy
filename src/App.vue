<script setup>
import {onMounted, ref,} from 'vue';

import BlogPost from './components/BlogPost.vue';
import LoadingSpinner from './components/LoadingSpinner.vue';
import PaginatePost from './components/PaginatePost.vue';

const posts = ref([]); //futuro arreglo que va a recibir la data del api
const postFavorito = ref('');
const maxPageContent = 5;
const inicio = ref(0);
const fin = ref(maxPageContent);
const loading = ref(true)

const selectPostFavorito = (title) =>{
  return postFavorito.value = title;
}

const next = ()=>{
  inicio.value += maxPageContent;
  fin.value += maxPageContent;     
}
const prev = ()=>{
  inicio.value -= maxPageContent;
  fin.value -= maxPageContent;     
}
/* 
onMounted(async ()=>{   
  try{
    const res = await fetch('https://jsonplaceholder.typicode.com/posts');
    posts.value  = await res.json();
  }catch(e){
    console.log(e);
  }finally{
    loading.value = false
  }
})
 */

fetch('https://jsonplaceholder.typicode.com/posts') 
  .then(res => res.json())
  .then(data => posts.value = data)
  .catch((e)=>{
    console.log(e);
  })
  .finally(()=> loading.value = false)

</script>
<template>
  <h1>Mi post favorito es: {{ postFavorito }}</h1>
  <PaginatePost
   class="mb-3"
   @next = "next"
   @prev = "prev"
   :inicio = "inicio"
   :fin = "fin"
   :maxLength = "posts.length"
   ></PaginatePost>

  <LoadingSpinner
    v-if="loading"
  />
   
  <BlogPost 
    v-else
    v-for="post in posts.slice(inicio,fin)"
    :key="post.id"
    :title="post.title" 
    :id="post.id"
    :body="post.body"
    @selectPostFavorito = "selectPostFavorito"
    class="mb-2"

  ></BlogPost>


</template>


<style>

</style>