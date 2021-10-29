<template>
  <v-dialog persistent v-model="dialog" max-width="600px">
    <v-card>
      <v-card-title>
        <span v-if="editedContact.id" class="text--h2">Edit Contact</span>
        <span v-else class="text--h2">New Contact</span>
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
                  v-model="editedContact.name"
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
                  v-model="editedContact.last_name"
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
                  v-model="editedContact.phone_number"
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
                  v-model="editedContact.email"
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
                  v-model="editedContact.country"
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
                  v-model="editedContact.city"
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
                  v-model="editedContact.address"
                  :error-messages="errors"
                  label="Address"
                  required
              ></v-text-field>
            </validation-provider>

              <v-btn text class="success mr-6 mt-4" @click="add()">Add contact</v-btn>
              <v-btn text class="red mt-4 white--text" @click="$emit('close')">Cancel</v-btn>

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
  props: ['dialog', 'editedContact'],
  components: {
    ValidationProvider,
    ValidationObserver
  },
  data() {
    return {
      inputRule: [
        v => v.length >= 1 || 'Field can not be empty'
      ]
    }
  },
  methods: {
    add() {
      console.log(this.editedContact.name);
      this.$emit('close');
    }
  }
}
</script>

<style scoped>

</style>
