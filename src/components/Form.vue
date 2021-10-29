<template>
  <v-dialog persistent v-model="dialog" max-width="600px">
    <v-card>
      <v-card-title>
        <span class="text--h2">{{ headerTitle }}</span>
      </v-card-title>

      <v-card-text>
        <v-form ref="formRef" class="px-5">
          <v-text-field
              v-model="editedContact.name"
              :rules="inputRule"
              required
              label="Name"></v-text-field>
          <v-text-field
              v-model="editedContact.last_name"
              :rules="inputRule"
              required
              label="Last Name"></v-text-field>

          <v-text-field
              v-model="editedContact.phone_number"
              :counter="9"
              :rules="phoneRule"
              label="Phone Number"
              required
          ></v-text-field>
          <v-text-field
              v-model="editedContact.email"
              :rules="emailRule"
              label="Email"
              required
          ></v-text-field>

          <v-text-field
              v-model="editedContact.country"
              :rules="inputRule"
              label="Country"
              required
          ></v-text-field>
          <v-text-field
              v-model="editedContact.city"
              :rules="inputRule"
              label="City"
              required
          ></v-text-field>
          <v-text-field
              v-model="editedContact.address"
              :rules="inputRule"
              label="Address"
              required
          ></v-text-field>

          <v-btn text class="success mr-6 mt-4" @click="add()">{{ buttonTitle }}</v-btn>
          <v-btn text class="red mt-4 white--text" @click="$emit('close')">Cancel</v-btn>

        </v-form>
      </v-card-text>
    </v-card>
  </v-dialog>
</template>

<script>

export default {
  name: "Form",
  props: ['dialog', 'editedContact'],
  data() {
    return {
      inputRule: [
        v => v.length >= 1 || 'Field can not be empty'
      ],
      emailRule: [
        v => v.length >= 1 || 'Field can not be empty',
        v => /^\w+([.-]?\w+)*@\w+([.-]?\w+)*(\.\w{2,3})+$/.test(v) || 'E-mail must be valid'
      ],
      phoneRule: [
        v => v.length === 9 || 'You must input 9 digits',
        v => new RegExp('^[0-9]*$').test(v) || 'Phone need to be 9 digits'
      ]
    }
  },
  computed: {
    buttonTitle() {
      return this.editedContact.id ? 'Edit contact' : 'Add contact'
    },
    headerTitle() {
      return this.editedContact.id ? 'Edit contact' : 'New contact'

    }
  },
  methods: {
    async add() {
      if (this.$refs.formRef.validate()) {
        const contact = {
          name: this.editedContact.name,
          last_name: this.editedContact.last_name,
          phone_number: this.editedContact.phone_number,
          email: this.editedContact.email,
          country: this.editedContact.country,
          city: this.editedContact.city,
          address: this.editedContact.address
        }

       let confirmation = confirm("Are you sure?");

        if (confirmation) {
          try {
            if (this.editedContact.id) {
              await this.editContact(contact, this.editedContact.id);
              this.$emit('close');
              this.$emit('reload');
            } else {
              await this.createContact(contact);
              this.$emit('close');
              this.$emit('reload');
            }
          } catch (e) {
            console.log(e);
          }
        }
      }

    },
    createContact(contact) {
      return this.axios.post(process.env.VUE_APP_API_REQUEST, contact, {
        headers: {
          'content-type': 'application/json',
        }
      });
    },
    editContact(contact, id) {
      return this.axios.put(`${process.env.VUE_APP_API_REQUEST}/${id}`, contact, {
        headers: {
          'content-type': 'application/json',
        }
      });
    }
  }
}
</script>

<style scoped>

</style>
