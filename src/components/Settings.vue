<template>
    <div>
        <button @click="$emit('back')" class="btn btn-light"><i class="material-icons">arrow_back</i></button>
        <button class="btn btn-light">Export</button>
        <button class="btn btn-danger">Delete All</button>
    </div>
</template>

<script>
export default {
    name: 'Settings'
}
</script>

<style>

</style>
