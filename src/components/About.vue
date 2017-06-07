<template>
  <div class="hello">
    <h1>{{ msg }} from <a href="https://www.reddit.com/r/oneliners/">Reddit</a></h1>
    <router-link to="/">Home</router-link>
  </div>
</template>

<script>
export default {
  name: 'hello',
  data () {
    return {
      msg: 'Woodpecker: a random one-line joke'
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}

a {
  color: #42b983;
}
</style>
