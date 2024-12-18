<script setup>

import BlogPost from './components/BlogPost.vue';
import { ref,computed } from 'vue'
import PaginasPost from './components/PaginasPost.vue';
import LoadingSpinner from './components/LoadingSpinner.vue';
import { onMounted } from 'vue';




// const posts =ref([
//   {title:"Post 1", id:1, body:"descripcion 1"},
//   {title:"Post 2", id:2, body:"descripcion 2"},
//   {title:"Post 3", id:3, body:"descripcion 3"},
//   {title:"Post 4", id:4, body:"descripcion 4"},
// ])

const posts = ref([]);

const favorito = ref("");

const cambiarFavorito = (title) => {
  favorito.value = title;
  // debemos de especificar que es lo que la funcion va a recibir y regresar
}


// const conectar=async() => { 
//   try{
//     const res= await fetch('https://jsonplaceholder.typicode.com/posts')
//     const data=await res.json();
//     post.value=data;


//   }catch(error){
//     console.log(error)
//   }
//  }

onMounted(async()=>{
  try{
    const res = await fetch('https://jsonplaceholder.typicode.com/posts')
    const data=await res.json();
    posts.value=data;
  }catch(error){
    console.log(error)
  }finally{
    loading.value=false;
  }
})

// fetch('https://jsonplaceholder.typicode.com/posts')
//   .then(res => res.json())
//   .then(data => {
//     posts.value = data
//   })
//   .finally(()=>(loading.value=false));

  const inicio=ref(0);
  const fin=ref(postxpage); 
  const postxpage=10;
  const loading=ref(true);


  const next=() => { 
    inicio.value=inicio.value+postxpage;
    fin.value=fin.value+postxpage;
  }
  
  const previous=() => { 
    inicio.value=inicio.value-postxpage;
    fin.value=fin.value-postxpage;
   } 

   const maxLength=computed(()=>posts.value.length)

</script>

<template>
  <LoadingSpinner class="mt-5" v-if="loading"></LoadingSpinner>
  <div class="contanier" v-else>

    <h1>Post Favoritos {{favorito || "Sin favoritos" }}</h1>

    <PaginasPost class="mb-2" @siguientePagina="next" @anteriorPagian="previous" :inicio :fin :maxLength></PaginasPost>

    <BlogPost class="mb-2" v-for="post in posts.slice(inicio,fin)" :key="post.id" :title="post.title" :id="post.id" :body="post.body"
      @cambiarFavoritos="cambiarFavorito"></BlogPost>
    <!-- de esta forma tenemos que donde está el @ es como se llama la funcion en el otro componenete, entre ""  es como se llama la funcion en su lugar de origen`^` -->
  </div>
      

</template> 