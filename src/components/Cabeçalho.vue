<!-- Componentes sempre começa com letra maiuscula! -->
    <script setup>
        const props = defineProps(['tarefasPendentes'])
</script> 
<template>
    <div class="containter">
        <header class="p-5 mb-4 mt-4 bg-light rounded-3">
    <h1>Minhas tarefas</h1>
    <p>
    Você possui {{ props.tarefasPendentes }} tarefas pendentes!
    </p>
    </header>
    </div>
</template>