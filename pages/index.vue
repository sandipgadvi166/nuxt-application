<template>
  <v-main class="grey lighten-3" color="white">
    <v-container fluid>
      <v-row>
        <v-col class="12">
          <v-card flat>
            <v-card-text class="text-center text--black">
              <h2 v-if="!error">Dashboard</h2>
              <h1 v-if="error">{{ error }}</h1>
            </v-card-text>
            <v-dialog
              v-model="dialog"
              fullscreen
              hide-overlay
              transition="dialog-bottom-transition"
            >
              <template v-slot:activator="{ on, attrs }">
                <v-btn v-bind="attrs" v-on="on" class="ml-8 mb-8">
                  new item</v-btn
                >
              </template>
              <v-card>
                <v-card-title>
                  <span class="headline"></span>
                </v-card-title>
                <v-card-text>
                  <v-container grid-list-md>
                    <v-layout wrap>
                      <v-flex xs12 sm6 md4>
                        <v-text-field
                          v-model="data.name"
                          label="name"
                        ></v-text-field>
                      </v-flex>
                      <v-flex xs12 sm6 md4>
                        <v-text-field
                          v-model="data.address"
                          label="Calories"
                        ></v-text-field>
                      </v-flex>
                      <v-flex xs12 sm6 md4>
                        <v-text-field
                          v-model="data.age"
                          label="Fat (g)"
                        ></v-text-field>
                      </v-flex>
                      <v-flex xs12 sm6 md4>
                        <v-text-field
                          v-model="data.sex"
                          label="Carbs (g)"
                        ></v-text-field>
                      </v-flex>
                      <v-flex xs12 sm6 md4>
                        <v-text-field
                          v-model="data.bill"
                          label="Protein (g)"
                        ></v-text-field>
                      </v-flex>
                    </v-layout>
                  </v-container>
                </v-card-text>
                <v-card-actions>
                  <v-spacer></v-spacer>
                  <v-btn color="blue darken-1" flat @click="dialog = false"
                    >Cancel</v-btn
                  >
                  <v-btn color="blue darken-1" flat @click.native="save"
                    >Save</v-btn
                  >
                </v-card-actions>
              </v-card>
            </v-dialog>

            <template>
              <v-data-table
                :headers="headers"
                :items="data"
                :items-per-page="10"
                class="elevation-1"
              >
              </v-data-table>
            </template>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </v-main>
</template>

<script>
import axios from 'axios'

export default {
  data() {
    return {
      headers: [
        { text: 'Name', value: 'name' },
        { text: 'Address', value: 'address' },
        { text: 'Date', value: 'date' },
        { text: 'Pet Name', value: 'pet_name' },
        { text: 'Age', value: 'age' },
        { text: 'sex', value: 'sex' },
        { text: 'Treatment', value: 'treatment' },
        { text: 'Bill', value: 'bill' },
        { text: 'Actions', value: 'action' },
      ],
      error: '',
      data: [],
      dialog: false,
    }
  },
  created() {
    axios
      .get('http://127.0.0.1:8001/api/register/')
      .then((response) => {
        this.data = response.data
      })
      .catch((error) => {
        this.error = error
        console.log(error)
      })
  },
}
</script>
