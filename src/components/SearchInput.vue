<template>
    <div class="search">
        <input class="search__input" type="text" name="search" :value="searchValue" @input="updateSearchValue($event.target.value)">
    </div>
</template>

<script>
export default {
    name: 'SearchInput',
    props: {
        searchValue: {
            type: String,
            required: true,
        },
    },
    emits: ['update:searchValue'],
    setup(props, { emit }) {
        const updateSearchValue = value => {
            emit('update:searchValue', value);
        }

        return { updateSearchValue };
    },
};
</script>

<style lang="scss" scoped>

    .search {
        width: 100%;
        padding: 10px 20px;
        margin-bottom: 10px;

        &.error {
            .search__input {
                color: #c53030;
            }
        }

        &__input {
            display: block;
            width: 100%;
            padding: 15px;
            color: rgb(17, 16, 16);
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
    }
</style>