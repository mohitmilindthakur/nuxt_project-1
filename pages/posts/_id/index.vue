<template>
  <div class="single-post-page">
    <section class="post">
      <h1>{{loadedPost.title}}</h1>
      <div class="post-details">
        <div class="post-detail">Last updated on the date somedate</div>
        <div class="post-detail">{{loadedPost.author}}</div>
        <p class="post-content">{{loadedPost.content}}</p>
      </div>
    </section>
    <section class="post-feedback">
      <p>Let me know what think about this</p>
    </section>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  asyncData(context) {
    console.log('ASYNC DATA');
    return axios
      .get(
        `https://nuxt-project-1-c3d95.firebaseio.com/posts/${context.route.params.id}.json`
      )
      .then(response => {
        console.log('SINGLE', response);
        return {
          loadedPost: response.data,
          testing: true
        };
      })
      .catch(error => {
        console.log("Error in getting post with ID", context.route.params.id);
        context.error(error);
      });
  }
};
</script>

<style>
.single-post-page {
  padding: 30px;
  text-align: center;
  box-sizing: border-box;
}

.post {
  width: 100%;
}

@media (min-width: 768px) {
  .post {
    width: 600px;
    margin: auto;
  }
}

.post-title {
  margin: 0;
}

.post-details {
  padding: 10px;
  box-sizing: border-box;
  border-bottom: 3px solid #ccc;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

@media (min-width: 768px) {
  .post-details {
    flex-direction: row;
  }
}

.post-detail {
  color: rgb(88, 88, 88);
  margin: 0 10px;
}

.post-feedback a {
  color: red;
  text-decoration: none;
}

.post-feedback a:hover,
.post-feedback a:active {
  color: salmon;
}
</style>