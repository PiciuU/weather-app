<template>
    <input type="text" id="search" name="search" :value="value" @input="handleChange">
</template>

<script>
export default {
    name: 'SearchInput',
    props: {
        value: {
            type: String,
            required: true,
        },
    },
    methods: {
        handleChange(e) {
            this.$emit('input', e.target.value);
        },
    },
};
</script>

<style lang="scss" scoped>
    input[type=text] {
        display: block;
        width: 100%;
        padding: 15px;

        color: #313131;
        font-size: 18px;
        letter-spacing: 1px;
        border:none;
        outline: none;
        box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.25);
        background-color: rgba(255, 255, 255, 0.35);
        border-radius: 12px;
        transition: .5s;

        &:focus {
            box-shadow: 0px 0px 12px rgba(0, 0, 0, 0.35);
            background-color: rgba(255, 255, 255, 0.6);
        }
    }
</style>
