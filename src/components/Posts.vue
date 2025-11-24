<template>
  <div class="post">
    <div class="timestamp">{{ post.timestamp }}</div>
    <p><strong>{{ post.title }}</strong></p>
    <img v-if="post.image" :src="post.image" :alt="post.alt || 'Post image'" />
    <p v-if="post.content">{{ post.content }}</p>
    <div class="like-button" @click="incrementLike">
      👍 Like ({{ post.likes }})
    </div>
  </div>
</template>

<script>
export default {
  props: {
    post: Object
  },
  methods: {
    incrementLike() {
      this.post.likes++;
    }
  }
};
</script>

<style scoped>

/* Individual post box */
.post {
  background-color: cadetblue;
  border-radius: 4px;
  width: 100%;
  padding: 1rem;
  position: relative;
  text-align: left;
  box-sizing: border-box;
}

/* Post image */
.post img {
  width: 100%;
  height: auto;
  border-radius: 10px;
  margin-top: 0.5rem;
  margin-bottom: 0.5rem;
}

/* Text inside post */
.post p {
  margin-top: 0.5rem;
}

/* Timestamp */
.timestamp {
  position: absolute;
  top: 10px;
  right: 10px;
  font-size: 1rem;
  color: #292929;
}
/* creates vertical space below the timestamp */
.post p:first-of-type {
  margin-top: 1.5rem;
}

/* Like button */
.like-button {
  margin-top: 0.5rem;
  color: #292929;
  cursor: pointer;
  display: flex;
  align-items: center;
  gap: 0.3rem;
}
.like-button:hover {
  color: rgb(36, 83, 107);
}

/* Demonstrating required selectors */
.post + .post {
  border-top: 3px solid #bbb; /* Adjacent sibling selector */
}
.posts-container > .post {
  box-shadow: 2px 2px 5px rgba(0,0,0,0.1); /* Child selector */
}
h2 ~ p {
  font-style: italic; /* General sibling selector */
}
/* Mobile-friendly posts */
@media (max-width: 600px) {
  .posts-container {
    max-width: 95%;
    padding: 0;
  }
  .post {
    width: 100%;
    border-radius: 12px;
    padding: 0.8rem;
  }
}
</style>