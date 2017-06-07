<template>
  <div class="hello">
    <h1>One-Line Joke</h1>
    <br/><br/>
    <h2>{{ joke }}</h2>
    <br/><br/>
    <router-link to="about">About</router-link>
  </div>
</template>

<script>
export default {
  name: 'hello',
  data: function () {
    return {
      joke: ''
    }
  },
  created: function () {
    this.fetchJoke()
  },
  methods: {
    fetchJoke: function () {
      const apiURL = 'https://www.reddit.com/r/oneliners.json'
      const xhr = new XMLHttpRequest()
      var self = this
      xhr.open('GET', apiURL)
      xhr.onload = function () {
        const data = JSON.parse(xhr.responseText)
        var joke
        do {
          const randomIndex = Math.floor(Math.random() * (20 - 0 + 1)) + 0
          joke = data.data.children[randomIndex].data
        } while (joke.stickied === true)
        self.joke = joke.title
      }
      xhr.send()
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1 {
  font-weight: bold;
}

h2 {
  font-weight: normal;
}

a {
  color: #42b983;
}
</style>
