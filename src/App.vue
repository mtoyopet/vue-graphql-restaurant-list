<template>
  <v-app>
    <v-container class="mt-5">
      <div class="display-2 text-center">チェーン店メモったろう君</div>
      <Graphql />
    </v-container>
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
