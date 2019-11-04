<template>
  <div class="container">
    <article>
      <h1 class="title">{{post.title}}</h1>
      <p>{{post.content}}</p>
    </article>
    <aside>
      <h3>Post you might enjoy</h3>
      <ul>
        <li v-for="post in relatedPosts" :key="post.id">
          <nuxt-link :to="{name: 'posts-id', params:{id:post.id}}">{{post.title}}</nuxt-link>
        </li>
      </ul>
    </aside>
  </div>
</template>
<script>
export default {
  data() {
    return {
      id: this.$route.params.id
    };
  },
  head() {
    return {
      title: this.post.title,
      meta: [
        { name: "twitter.title", content: "Nuxt fundamentals by Vue" },
        { name: "twitter.description", content: "Nuxt + Vue School = *" },
        { name: "twitter.image", content: "https://i.imgur.com/UYP2umJ.png" },
        { name: "twitter.card", content: "summary_large" }
      ]
    };
  },
  computed: {
    post() {
      return this.$store.state.posts.all.find(post => post.id == this.id);
    },
    relatedPosts() {
      return this.$store.state.posts.all.filter(post => post.id !== this.id);
    }
  }
};
</script>
<style scoped>
.container {
  display: flex;
  justify-content: space-between;
  line-height: 1.5;
}
article * {
  margin-bottom: 1rem;
}
aside {
  min-width: 280px;
  max-width: 280px;
  padding-left: 2rem;
}
.title {
  font-size: 2rem;
}
</style>