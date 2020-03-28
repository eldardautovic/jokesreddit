<template>
  <div id="app">
    <header>
      <h1>/r/jokes</h1>
    </header>
    <main v-if="isLoaded">
      <div class="joke" v-for="joke in jokeDetails" :key="joke.data.id">
        <a :href="joke.data.url">
          <h1>{{joke.data.title}}</h1>
        </a>
        <div class="joke-author">
          <p>Author: {{joke.data.author}}</p>
        </div>
        <div class="joke-stats">{{joke.data.ups}} Upvotes | {{joke.data.num_comments}} Comments</div>
      </div>
      <Footer />
    </main>
    <div v-else>
      <LoadingSpinner />
    </div>
  </div>
</template>

<script>
import LoadingSpinner from "./components/LoadingSpinner.vue";
import Footer from "./components/footer.vue";

export default {
  name: "App",
  components: {
    Footer,
    LoadingSpinner
  },
  data() {
    return {
      jokeDetails: [],
      isLoaded: false
    };
  },
  created() {
    fetch(`https://www.reddit.com/r/Jokes.json?limit=20`)
      .then(response => response.json())
      .then(data => {
        this.jokeDetails = data.data.children;
        this.jokeDetails.shift();
        this.isLoaded = true;
      });
  }
};
</script>
<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  background-image: linear-gradient(to top, #a18cd1 0%, #fbc2eb 100%);
}

header h1 {
  min-height: 20vh;
  display: flex;
  justify-content: center;
  align-content: center;
  font-family: sans-serif;
  color: #2f2f2f;
  font-size: 50px;
  padding-top: 50px;
}

main {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

.joke {
  width: 300px;
  height: 300px;
  box-shadow: 10px 10px 13px -8px rgba(0, 0, 0, 0.55);
  border-radius: 15px;
  display: flex;
  flex-direction: column;
  text-align: center;
  justify-content: center;
  align-content: center;
  font-family: sans-serif;
  color: #2f2f2f;
  margin: 20px;
  background-color: white;
}

.joke h1 {
  font-size: 15px;
}

.joke a {
  text-decoration: none;
  color: currentColor;
  transition: 0.5s ease;
}

.joke a:hover {
  opacity: 0.8;
}

.joke-author {
  margin-top: 5%;
}

.joke-stats {
  margin-top: 2%;
}
</style>
