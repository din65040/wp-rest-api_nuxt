<template>
  <div class="container">
    <div>
      <h1 class="title">
        wp-rest-api_nuxt
      </h1>

      <article v-for="post in posts" :key="post.id">
        <n-link :to="{ path: '/posts/' + post.id }">
          <h2>{{ post.title.renderd }}</h2>
        </n-link>
        <div v-html="post.content.rendered"></div>
      </article>

      <div class="links">
        <a href="https://nuxtjs.org/" target="_blank" class="button--green">
          Documentation
        </a>
        <a
          href="https://github.com/nuxt/nuxt.js"
          target="_blank"
          class="button--grey"
        >
          GitHub
        </a>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      post: []
    };
  },
  async asyncData({ $axios }) {
    const { data } = await $axios.get("/posts?_embed");
    return { posts: data };
  }
};
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont,
    "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 50px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
