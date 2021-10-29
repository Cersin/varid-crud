<template>
  <v-dialog v-model="dialog" max-width="600px">
    <template v-slot:activator="{ on }">
      <v-btn text v-on="on" class="primary">Add new contact</v-btn>
    </template>
    <v-card>
      <v-card-title>
        <span class="text--h2">New Contact</span>
      </v-card-title>

      <v-card-text>
        <validation-observer ref="observer">
          <v-form class="px-5">
            <validation-provider
                v-slot="{ errors }"
                name="Name"
                :rules="{
          required: true
            }">
              <v-text-field
                  v-model="name"
                  required
                  :error-messages="errors"
                  label="Name"></v-text-field>
            </validation-provider>

            <validation-provider
                v-slot="{ errors }"
                name="Last Name"
                :rules="{
          required: true
            }">
              <v-text-field
                  v-model="last_name"
                  required
                  :error-messages="errors"
                  label="Last Name"></v-text-field>
            </validation-provider>

            <validation-provider
                v-slot="{ errors }"
                name="Phone"
                :rules="{
          required: true,
          digits: 9,
          regex: '^[0-9]*$'
            }">
              <v-text-field
                  v-model="phone_number"
                  :counter="9"
                  :error-messages="errors"
                  label="Phone Number"
                  required
              ></v-text-field>
            </validation-provider>


            <validation-provider
                v-slot="{ errors }"
                name="Email"
                :rules="{
          required: true,
          email: true
            }"
                >
              <v-text-field
                  v-model="email"
                  :error-messages="errors"
                  label="Email"
                  required
              ></v-text-field>
            </validation-provider>

            <validation-provider
                v-slot="{ errors }"
                name="Country"
                :rules="{
          required: true,
            }"
            >
              <v-text-field
                  v-model="country"
                  :error-messages="errors"
                  label="Country"
                  required
              ></v-text-field>
            </validation-provider>

            <validation-provider
                v-slot="{ errors }"
                name="City"
                :rules="{
          required: true,
            }"
            >
              <v-text-field
                  v-model="city"
                  :error-messages="errors"
                  label="City"
                  required
              ></v-text-field>
            </validation-provider>

            <validation-provider
                v-slot="{ errors }"
                name="Address"
                :rules="{
          required: true,
            }"
            >
              <v-text-field
                  v-model="address"
                  :error-messages="errors"
                  label="Address"
                  required
              ></v-text-field>
            </validation-provider>

              <v-btn text class="success mr-6 mt-4">Add contact</v-btn>
              <v-btn text class="red mt-4 white--text" @click="close">Cancel</v-btn>

          </v-form>
        </validation-observer>
      </v-card-text>
    </v-card>
  </v-dialog>
</template>

<script>
import {required, digits, regex, email} from 'vee-validate/dist/rules'
import {extend, setInteractionMode, ValidationProvider, ValidationObserver} from 'vee-validate';

setInteractionMode('eager')

extend('required', {
  ...required,
  message: '{_field_} can not be empty',
})

extend('digits', {
  ...digits,
  message: '{_field_} needs to be {length} digits. ({_value_})',
})

extend('regex', {
  ...regex,
  message: '{_field_} {_value_} does not match {regex}',
})

extend('email', email);

export default {
  name: "Form",
  components: {
    ValidationProvider,
    ValidationObserver
  },
  data() {
    return {
      dialog: false,
      inputRule: [
        v => v.length >= 1 || 'Field can not be empty'
      ],
      name: "",
      last_name: "",
      phone_number: "",
      email: "",
      country: "",
      city: "",
      address: ""
    }
  },
  methods: {
    close() {
      this.dialog = false;
      console.log('closing');
    }
  }
}
</script>

<style scoped>

</style>
