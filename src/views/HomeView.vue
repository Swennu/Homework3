<template>
<div>
    

    <main class="index">
      <h1 id="mainHeader">Posts</h1>

      <section class="posts-container">
        <Post v-for="(post, index) in posts" :key="index" :post="post" @like="incrementLike(index)"/>
      </section>
    </main>
  </div>
</template>

<script>
// @ is an alias to /src
import Post from '@/components/Posts.vue';

export default {
  name: 'HomeView',
  components: { Post },
  data() {
    return {
      posts: [],
      loading: true,
    };
  },
  mounted() {
    fetch('/data/posts_temp.json')
      .then(res => res.json())
      .then(data => {
        this.posts = data.map(post => ({
          ...post,
          likes: post.likes || 0
        }));
        this.loading = false;
      })
      .catch(err => {
        console.error('Error fetching posts:', err);
        this.loading = false;
      });
  },
   methods: {
    incrementLike(index) {
      this.posts[index].likes++;
    }
  }
};

</script>

<style scoped>
/* Header */
#mainHeader {
  color: rgb(35, 59, 59);
  margin-bottom: 1rem;
}
/* Page Layouts */
div > h1 {
    text-align: center;
    font-size: 1.8rem;
}

h1 + p {
 text-decoration-line: underline;
}

h1 ~ p {
    font-size: small;
    color: rgb(35, 59, 59);
    font-style: italic;
}

main.add-post, main.login, main.index {
  padding: 1rem;
  text-align: center;
  min-height: 80vh; /* Ensures footer stays at the bottom */
}

/* Forms */
.post-form, .login-form {
  max-width: 400px;
  width: 90%;
  margin: 2rem auto;
  padding: 1rem;
  border-radius: 4px;
  width: 300px;
  background-color: cadetblue;
  box-sizing: border-box;
}
.post-form input, .post-form textarea, .login-form input {
  width: 100%;
  padding: 0.5rem;
  margin-bottom: 1rem;
  border: 1px solid #ccc;
  border-radius: 4px;
  resize: none;
  box-sizing: border-box;
}
.post-form input[type="text"] {
  font-weight: bold;
}
.post-form input[type="submit"], .login-form input[type="submit"] {
  padding: 0.5rem 1rem;
  background-color: #cecccc;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}
.post-form input[type="submit"]:hover, .login-form input[type="submit"]:hover {
  background-color: #918f8f;
}

/* Login fields */
.login-form input[type="text"], .login-form input[type="password"] {
  width: 100%;
  padding: 0.5rem 1rem;
  border: 1px solid #ccc;
  border-radius: 4px;
  margin: 0.5rem auto;
  box-sizing: border-box;
}

/* Responsive */
@media (max-width: 600px) {
  nav ul {
    flex-direction: column;
    align-items: center;
  }
  .post-form {
    width: 90%;
    margin: 1rem auto;
  }
  .login-form {
  max-width: 300px;
  min-width: 200px;
  width: 90%;
  margin: 1rem auto;
  }
}

.posts-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1rem;
  margin: 1rem auto;
  width: 100%;
  max-width: 600px;
  overflow-y: auto;       /* vertical scroll only */
  overflow-x: hidden;     /* no horizontal scrolling */
  max-height: 75vh;
  padding: 0 0.5rem;
  box-sizing: border-box;
}
</style>
