<template>
  <v-row
      class="py-8"
      justify="center"
      >
        <v-col
          cols="12"
        >
          <BlogTable :blogs="blogs" :loading="loading"/>
      </v-col>
  </v-row>
</template>
<script>
export default {
    data(){
      return {
        blogs: [],
        loading: true
      };
    },
    computed:{
    },
    methods: {
      loadBlogs: function(){
        this.loading = true;
        this.$axios.$get('https://gorillalogic.com/wp-json/wp/v2/posts?_embed').then(response => {
          this.blogs = response.map(blog => {
            return {
              title: blog.title.rendered,
              description: blog.excerpt.rendered.replace(/(<[^>]*>)|\[(.*)\]/gm, '') + '...',
              imageUrl: blog._embedded['wp:featuredmedia'][0].media_details.sizes.medium_large.source_url
            }
          });
          this.loading = false;
        });
      }
    },
    created(){
      this.loadBlogs();
    }
  }
</script>
