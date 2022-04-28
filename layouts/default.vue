<template>
  <v-app id="inspire">
    <v-app-bar app>
      <img class="mr-3" src="/gorillalogic.png" height="40"/>
      <v-toolbar-title>Gorilla Logic Blog Entries</v-toolbar-title>
    </v-app-bar>

    <v-main>
      <v-container>
        <nuxt />
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: "default"
}
</script>
