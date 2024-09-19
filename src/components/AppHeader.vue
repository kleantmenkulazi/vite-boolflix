<script>
  import { store } from '../store.js';
  // my-component.js
export default {
  data() {
    return {
      store
    };
  },
  methods: {
    
  }
}
</script>

<template>
  <div>
    <div>
      <form @submit.prevent="$emit('search')">
        <input v-model="store.searchText" type="text" placeholder="Cerca info...">
        <button type="submit">
          Cerca
        </button>
      </form>
    </div>
    <div>
      <input v-model="store.searchText" type="text" placeholder="Cerca info...">
      <button @click="$emit('search')">
        Cerca
      </button>
    </div>
  </div>
</template>

<style scoped>

</style>
