<template>
  <h1>this is second child</h1>
  <third />
</template>

<script>

import third from './child3.vue'

export default {
  name: 'second-child',
  components: {
    third
  }
}
</script>

<style>
</style>