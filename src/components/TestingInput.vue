<template>
    <input type="text"
    :value="name"
    :id="id"
    @input="$emit('update:name', $event.target.value)"
    required
    >
</template>

<script>
export default {
    props: {
        name: {
            type: String,
            default: ''
        },
        id: {
            type: String,
            default: ''
        }
    }
}
</script>

<style scoped>

</style>