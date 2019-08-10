<template>
    <div>
        <input @input="onInput" />
    </div>
</template>

<script>
export default {
    methods: {
        onInput(event) {
            this.$emit("termChange", event.target.value);
        }
    }
};
</script>

<style lang="scss" scoped>
</style>