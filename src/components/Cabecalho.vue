<script setup>
    const props = defineProps(['tarefasPend'])
</script>
<template>
    <div class="container">
        <header class="p-5 mb-4 mt-4 bg-light rounded-3">
            <h1>Minhas Tarefas</h1>
            <p>
                Você possui {{ props.tarefasPend }} tarefas pendentes
            </p>
        </header>
    </div>
</template>