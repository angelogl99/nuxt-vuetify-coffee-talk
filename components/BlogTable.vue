<template>
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
</template>
<script>
export default {
  props: ['blogs', 'loading'],
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
      };
    },
  }
</script>
