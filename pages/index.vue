<template>
  <div>
    <!-- connection check -->
    <div v-if="$nuxt.isOffline">You are offline</div>
    <!-- <Tutorial /> -->
    <!-- refreshing data -->
    <div>{{ content }}</div>
     <h1>I am rendered on the {{ renderedOn }} side</h1>
    <button @click="refresh">Refresh</button>
  </div>
</template>

<script lang="ts">
  import Vue from 'vue'

  export default Vue.extend({
    name: 'IndexPage',
    asyncData() {
      return {
        content: 'Created at: ' + new Date(),
        renderedOn: process.client ? 'client' : 'server'
      }
    },
    methods: {
      refresh() {
        this.$nuxt.refresh()
      },
    },
    mounted() {
      this.$nextTick(() => {
        this.$nuxt.$loading.start()
        setTimeout(() => this.$nuxt.$loading.finish(), 500)
      })
    }
  })

</script>
