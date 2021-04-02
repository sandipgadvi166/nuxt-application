<template>
  <v-main class="pl-1 pr-1">
    <v-container>
      <v-row class="pt-1">
        <v-col cols="12" sm="8">
          <v-card class="pa-2">
            <v-form v-model="valid">
              <v-container>
                <v-row>
                  <v-col cols="6" md="4">
                    <v-text-field
                      v-model="firstname"
                      :rules="nameRules"
                      :counter="10"
                      label="First name"
                      required
                    ></v-text-field>
                  </v-col>

                  <v-col cols="6" md="4">
                    <v-text-field
                      v-model="lastname"
                      :rules="nameRules"
                      :counter="10"
                      label="Last name"
                      required
                    ></v-text-field>
                  </v-col>

                  <v-col cols="6" md="4">
                    <v-text-field
                      v-model="form.petname"
                      :rules="nameRules"
                      label="Pet name"
                      required
                    ></v-text-field>
                  </v-col>

                  <v-col cols="6">
                    <v-select
                      v-model="form.select"
                      :items="Ditems"
                      :rules="[(v) => !!v || 'Item is required']"
                      label="Sex"
                      required
                    ></v-select>
                  </v-col>
                  <v-spacer></v-spacer>
                  <v-col cols="6">
                    <v-text-field
                      v-model="form.address"
                      :rules="emailRules"
                      label="Address"
                      required
                    ></v-text-field>
                  </v-col>
                  <v-col cols="6">
                    <v-dialog
                      ref="dialog"
                      v-model="modal"
                      :return-value.sync="form.date"
                      persistent
                      width="290px"
                    >
                      <template v-slot:activator="{ on, attrs }">
                        <v-text-field
                          v-model="form.date"
                          label="Picker in dialog"
                          prepend-icon="mdi-calendar"
                          readonly
                          v-bind="attrs"
                          v-on="on"
                        ></v-text-field>
                      </template>
                      <v-date-picker v-model="form.date" scrollable>
                        <v-spacer></v-spacer>
                        <v-btn text color="primary" @click="modal = false">
                          Cancel
                        </v-btn>
                        <v-btn
                          text
                          color="primary"
                          @click="$refs.dialog.save(date)"
                        >
                          OK
                        </v-btn>
                      </v-date-picker>
                    </v-dialog>
                  </v-col>
                  <v-col cols="6">
                    <v-text-field
                      v-model="form.age"
                      :rules="emailRules"
                      label="Age"
                      required
                    >
                    </v-text-field>
                  </v-col>
                  <v-col cols="6">
                    <v-text-field
                      v-model="form.treatment"
                      :rules="emailRules"
                      label="Treatment"
                      required
                    >
                    </v-text-field>
                  </v-col>
                  <v-col cols="6">
                    <v-text-field
                      v-model="form.bill"
                      :rules="emailRules"
                      label="Bill"
                      required
                    >
                    </v-text-field>
                  </v-col>
                  <v-col cols="12">
                    <v-btn text color="primary" @click="save"> OK </v-btn>
                  </v-col>
                </v-row>
              </v-container>
            </v-form>
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
      firstname: '',
      lastname: '',
      form: {
        name: '',
        petname: '',
        address: '',
        age: '',
        treatment: '',
        bill: '',
        date: new Date().toISOString().substr(0, 10),
        select: null,
        name: '',
      },
      text: ['web', 'shop', 'videos', 'images', 'news'],
      modal: false,
      Ditems: ['male', 'female'],
    }
  },
  methods: {
    async save() {
      this.form.name = this.firstname + ' ' + this.lastname

      await this.$axios
        .$post('http://127.0.0.1:8001/api/register', this.form)
        .then((res) => {
          console.log(res.data)
        })
        .catch((error) => {
          console.log(error)
        })
    },
  },
}
</script>