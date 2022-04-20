<template>
  <v-app :style="{ background: $vuetify.theme.themes.dark.background }">
    <!-- <v-container fluid> -->
      <input type="text" v-model="text">
      <h3>Nama : {{  text  }}</h3>
    <!-- </v-container> -->
  </v-app>
</template>

<script>
  export default {
    name: 'HomeTest',
    data() {
      return{
        text: "Im Heri"
      }
    },
  }
</script>
