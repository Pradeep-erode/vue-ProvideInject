<template>
    <h1>This is third child</h1>
    <h1>I am from parent to third child - {{ deepname }}</h1>
    <h1>I am from parent to third child C-provide and inject - {{ rewValue }}</h1>
</template>

<script>

import { inject } from 'vue'

export default {
    name: 'third-child',
    //option api
    inject: ['deepname'],

    //composition API
    setup() {

        const rewValue = inject('Comp_Name', 'default name')

        return {
            rewValue
        }
    }
}
</script>

<style>
</style>