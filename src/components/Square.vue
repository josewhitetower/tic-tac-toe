<template>
    <button class="square">
        {{ value }}
    </button>
</template>

<script>
export default {
    name: 'Square',
    props: {
        values: {
            type: String,
            default: '',
        },
    },
    data() {
        return {};
    },
};
</script>

<style>

</style>
