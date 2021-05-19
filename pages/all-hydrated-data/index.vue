
<template>
  <div class="container">
    <Posts :posts="asyncDataPosts" :color="'red'"></Posts>
  </div>
</template>

<script>
import LazyHydrate from 'vue-lazy-hydration';

export default {
  components: {
    LazyHydrate
  },

  serverData() {
    return {
      serverDataPosts: []
    }
  },

  async asyncData(context) {

    // const data = await fetch('https://api.nuxtjs.dev/posts').then(res => res.json())

    // get the data from server.
    // this gets 5000 objects woth total size of 822KB
    const data = await fetch('https://jsonplaceholder.typicode.com/photos').then(res => res.json())

    const totalSize = data.length;

    const numberOfItemsInServerData = 0;

    // set some of the data into the $staticData object that will be used only in render time on server (SSR)
    context.$staticData.serverDataPosts = data.slice(0, numberOfItemsInServerData);

    // set some of the data into regular data that will be returned in __NUXT__.data[0]
    // this will be used for hydration on client
    // Example: Charts data
    return {
      asyncDataPosts: data.slice(numberOfItemsInServerData, totalSize)
    }
  },

  mounted() {
    const size = new TextEncoder().encode(JSON.stringify(window.__NUXT__)).length
    const kiloBytes = size / 1024;
    console.log("🚀 ~ file: index.vue ~ line 56 ~ mounted ~ kiloBytes", kiloBytes)
    const megaBytes = kiloBytes / 1024;
  }
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;

  justify-content: center;
  align-items: center;
  text-align: center;
}
</style>
