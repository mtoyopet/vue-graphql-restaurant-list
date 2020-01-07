<template>
  <v-app>
    <Graphql />
  </v-app>
</template>

<script>
  import Graphql from './components/Graphql.vue'
  export default {
    name: 'App',
    components: {
      Graphql
    },

    data: () => ({
      //
    }),
  };
</script>
