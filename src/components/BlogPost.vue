<script setup>

// defineProps(['title'])

defineProps({
    title:String,
    id:Number,
    body:{
        type:String,
        default:"Sin descripcion",
    },
});

// Esta manera es una de las muchas que hay para poder hacer el llamado de las fuciones desde otro lado, una de las mejores
const emit= defineEmits(["cambiarFavoritos"]);

</script>

<template>
    <div class="card">
        <div class="card-body">
           <h5 class="card-title">
            {{id}} - {{title}}
           </h5>
           <p>
               {{ body }}
            </p>
            <button @click="emit('cambiarFavoritos',title)"
            class="btn btn-outline-primary"
            >
            <!-- arriba ya no se le debe de poner el signo de $ al emit porque ya fue declarada la funcion si es que la vamos a ocupar mas de una vez -->
                Add
            </button> 
        </div>
    </div>
</template> 