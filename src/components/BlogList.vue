<template>
  <div>
    <p>{{ title }}</p>
    <table>
      <tr v-for="blog in blogs" :key="blog">
        <td @click="show_blog(blog.id)">{{ blog.title }}</td>
        <!-- <td>
          <router-link :to="{name: 'BlogDetail', query: { id: blog.id } }"> {{ blog.title }}</router-link>
        </td> -->
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      title: '博客列表页',
      blogs: [

      ]
    }
  },
  mounted() {
    this.$http.get('/test/interface/blogs/all').then((response) => {
      console.info(response.body)
      this.blogs = response.body.blogs
    }, (response) => {
      console.error(response)
    })
  },
  methods: {
    show_blog: function(blog_id) {
      this.$router.push({ name: 'BlogDetail', query: { id: blog_id }})
    }
  }
}
</script>

<style>
</style>
