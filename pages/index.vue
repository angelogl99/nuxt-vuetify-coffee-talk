<template>
  <v-app id="inspire">
    <v-app-bar app>
      <v-toolbar-title>Gorilla Logic Blog Entries</v-toolbar-title>
    </v-app-bar>

    <v-main>
      <v-container>
          <v-row
              class="py-8"
              justify="center"
              >
                <v-col
                  cols="12"
                >
                  <v-card >
                    <v-data-table
                    :headers="headers"
                    :items="blogs"
                    :items-per-page="5"
                    :loading="loading"
                    class="elevation-1"
                    >
                      <template v-slot:[`item.imageUrl`]="{ item }">
                        <div class="p-2">
                          <v-img :src="item.imageUrl" :alt="item.name" height="100px" width="100px" contain></v-img>
                        </div>
                      </template>
                    </v-data-table>
                  </v-card>
                </v-col>
            </v-row>
        </v-container>
    </v-main>
  </v-app>
</template>
<script>
export default {
    data(){
      return {
        headers: [
          {
            text: 'Image',
            value: "imageUrl",
            sortable: false
          },
          {
            text: 'Title',
            value: 'title',
            width: '150px'
          },
          {
            text: 'Description',
            value: 'description',
            sortable: false
          },
          { text: 'Actions', value: 'actions', sortable: false },
        ],
        footerProps: {
          'items-per-page-options': [3, 5, 10],
        },
        blogs: [],
        loading: true,

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
