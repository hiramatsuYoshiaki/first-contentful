<template>
  <div class="container">
    contentful
    <div v-if="posts.length">
      <ul v-for="(post, i) in posts" :key="i">
        <!-- {{JSON.stringify(post)}} -->

        <li>title:{{ post.fields.title }}</li>
        <li>slug:{{ post.fields.slug }}</li>
        <li>heroImage:{{ post.fields.heroImage }}</li>
        <li>body:{{ post.fields.body }}</li>
        <li>author:{{ post.fields.author }}</li>
        <li>publishDate:{{ post.fields.publishDate }}</li>
        <li>tags:{{ post.fields.tags }}</li>
        <li>heroImage/sys/space/sys:{{ post.fields.heroImage.sys.space.sys }}</li>
        <li>heroImage/fields:{{ post.fields.heroImage.fields }}</li>
        <li>heroImage/fields/file/url:{{ post.fields.heroImage.fields.file.url }}</li>

        <li>-------------------------------------------------</li>

        <!-- <li>{{ post.fields.body }}</li>
        <li>{{ post.fields.publishDate }}</li>-->
        <ul>
          <img
            :src="post.fields.heroImage.fields.file.url"
            :alt="post.fields.heroImage.fields.title"
            :aspect-ratio="16/9"
            max-width="400"
            max-height="225"
          />
          <!-- <li>{{ post.fields.body }}</li>
          <li>{{ post.fields.publishDate }}</li>-->
        </ul>
      </ul>
      {{JSON.stringify(posts)}}
    </div>
  </div>
</template>

<script>
import client from "~/plugins/contentful";

export default {
  async asyncData({ env }) {
    let posts = [];
    await client
      .getEntries({
        content_type: env.CTF_BLOG_POST_TYPE_ID,
        order: "-fields.publishDate"
      })
      .then(res => (posts = res.items))
      .catch(console.error);
    return { posts };
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

/* .title {
  font-family: "Quicksand", "Source Sans Pro", -apple-system, BlinkMacSystemFont,
    "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
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
} */
</style>
