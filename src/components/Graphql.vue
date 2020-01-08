<template>
  <v-container>
    <Form />
    <v-row>
      <v-col 
        v-for="item in restaurants" 
        v-bind:key="item.id" 
        cols="3"
      >
        <v-card
          class="mb-2"
          max-width="400"
          cols="3"
        >
          <v-card-title>{{ item.name }}</v-card-title>
          <v-card-text class="text--primary">
            <div>{{ item.description }}</div>
          </v-card-text>
          <v-btn
            icon
            small
            class="red--text mr-2"
            v-on:click="deleteRestaurant(item.id)"
          >
            <v-icon>mdi-delete</v-icon>
          </v-btn>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
  import axios from "axios";
  import Form from './Form.vue'

  export default {
    name: 'graphql',
    components: {
      Form
    },
    data() {
      return {
        restaurants: [],
        apiURL: "https://dry-citadel-76623.herokuapp.com/graphql"
      };
    },
    mounted() {
      this.getRestaurants()
    },
    methods: {
      async deleteRestaurant(id){
        try {
          await axios({
          method: "POST",
          url: this.apiURL,
          data: {
            query: `
              mutation {
                deleteRestaurant(input: {
                  where: {
                    id: ${id}
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
          this.getRestaurants()
        } catch (error) {
          // console.error(error);
        }
      },
      async getRestaurants(){
        try {
          var result = await axios({
            method: "POST",
            url: this.apiURL,
            data: {
              query: `
                query getRestaurants {
                  restaurants {
                    id
                    name
                    description
                  }
                }
              `
                }
            });
            // console.log(result)
            this.restaurants = result.data.data.restaurants;
        } catch (error) {
          // console.error(error);
        }
      }      
    }
  }
</script>