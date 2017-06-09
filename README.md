# woodpecker

Woodpecker is a simple web site implemented using [Vue.js](https://vuejs.org) that shows a random joke from Reddit.

### Background

This project is part of [52projects](https://donny.github.io/52projects/) and the new stuff that I learn through this project: [Vue.js](https://vuejs.org).

### Project

Woodpecker fetches a random one-line joke on every refresh from the trending page of Reddit [/r/oneliners](https://www.reddit.com/r/oneliners/). Woodpecker displays the one-line joke on the page. The screenshot of Woodpecker can be found below:

![Screenshot](https://raw.githubusercontent.com/donny/woodpecker/master/screenshot.png)

### Implementation

Woodpecker is scaffolded using [vue-cli](https://github.com/vuejs/vue-cli) and it was bootstrapped using the following command: `vue init webpack woodpecker`. Woodpecker was deployed on [Netlify](https://www.netlify.com). We created a route for a new About page with the following Vue.js component:

```javascript
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
```

The main code to fetch the joke is implemented in [`Home.vue`](https://github.com/donny/woodpecker/blob/master/src/components/Home.vue) and it can be seen below:

```javascript
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
```

### Conclusion

...
