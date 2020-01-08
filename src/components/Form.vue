<template>
  <v-container>
    <v-form>
    <v-container>
      <v-row>
        <v-col
          cols="12"
          md="3"
        >
          <v-text-field
            v-model="name"
            label="お店の名前"
          ></v-text-field>
        </v-col>
        <v-col
          cols="12"
          md="6"
        >
          <v-text-field
            v-model="description"
            label="どんなお店？"
          ></v-text-field>
        </v-col>
        <v-col>
          <v-btn 
            class="primary"
            v-on:click="createRestaurant"
            align="center"
            >
            追加する
          </v-btn>
        </v-col>
      </v-row>
    </v-container>
  </v-form>
  </v-container>
</template>

<script>
  import axios from "axios";
  export default {
    name: 'Form',
    data: () => ({
      name: "",
      description: ""
    }),
    methods: {
      async createRestaurant(){
        try {
          await axios({
          method: "POST",
          url: "https://dry-citadel-76623.herokuapp.com/graphql",
          data: {
            query: `
              mutation {
                createRestaurant(input: {
                  data: {
                    name: "${this.name}",
                    description: "${this.description}"
                  }
                }) {
                  restaurant {
                    name
                    description
                  }
                }
              }
            `
            }
          });
          this.name = ""
          this.description = ""
          this.$parent.getRestaurants()
        } catch (error) {
          // console.error(error);
        }
      }, 
    }
};
</script>
