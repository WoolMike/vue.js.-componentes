<script setup>
import {ref} from 'vue'
const emit=defineEmits(["siguientePagina","anteriorPagian"]);
defineProps(['inicio','fin','maxLength'])


const siguiente=() => { 
    emit("siguientePagina");
 }

const anterior=() => { 
    emit("anteriorPagian");
    
 }



</script>

<template>
    <div class="btn-group" role="group" aria-label="Basic example">
        <button type="button" class="btn btn-primary" @click="anterior" :disabled="inicio===0">Previous</button>
        <button type="button" class="btn btn-primary" @click="siguiente" :disabled="fin===maxLength">Next</button>
    </div>
</template>    