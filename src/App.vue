<template>
    <div class="main-app">
      <v-watch
          v-for="watch in watches"
          :key="watch"
      />
      <button class="add" @click="add">+</button>
    </div>

</template>

<script>

import VWatch from "@/components/v-Watch.vue";

export default {
  name: 'App',
  components: {
    VWatch
  },
  data() {
    return {
      watches: 3, // настраивает количество секундомеров
    }
  },
  methods: {
    add() {
      this.watches += 1
    }
  }
}
</script>
