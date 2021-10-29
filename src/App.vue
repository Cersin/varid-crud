<template>
  <v-app id="inspire">
    <Form :dialog="dialogOpen" :editedContact="editContact" @close="closeDialog"></Form>

    <v-app-bar app>
      <v-toolbar-title>Application</v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn text class="primary"
             @click="newContact">Add new contact
      </v-btn>
    </v-app-bar>

    <v-main>
      <Table @editItem="editItem" :data="contacts"></Table>
    </v-main>
  </v-app>
</template>

<script>
import Table from "@/components/Table";
import Form from "@/components/Form";

export default {
  components: {Table, Form},
  data() {
    return {
      drawer: null,
      dialogOpen: false,
      contacts: [],
      editContact: {
        name: "",
        last_name: "",
        phone_number: "",
        email: "",
        country: "",
        city: "",
        address: ""
      },
      defaultContact: {
        name: "",
        last_name: "",
        phone_number: "",
        email: "",
        country: "",
        city: "",
        address: ""
      }
    }
  },
  created() {
    this.initialize();
  },
  methods: {
    closeDialog() {
      this.dialogOpen = false;
    },
    editItem(item) {
      this.editContact = item;
      this.dialogOpen = true;
    },
    newContact() {
      this.editContact = this.defaultContact
      this.dialogOpen = true;
    },
    initialize() {
      this.contacts = [
        {
          "id": 547,
          "name": "Mareczek",
          "last_name": "Winiarski",
          "phone_number": "3434242",
          "email": "test0@mail.com",
          "country": "country0",
          "city": "city0",
          "address": "address0",
          "created_at": "2021-10-28T15:36:17.000000Z",
          "updated_at": "2021-10-28T19:35:27.000000Z"
        },
        {
          "id": 546,
          "name": "Johny",
          "last_name": "Bravo",
          "phone_number": "123456789",
          "email": "j@j.pl",
          "country": "Portugalia",
          "city": "Lizbona",
          "address": "prtthha 10/4",
          "created_at": "2021-10-28T14:57:46.000000Z",
          "updated_at": "2021-10-28T14:57:46.000000Z"
        },
        {
          "id": 545,
          "name": "Piotr",
          "last_name": "Winiarek",
          "phone_number": "654321987",
          "email": "pio@pio.pl",
          "country": "Chorwacja",
          "city": "Split",
          "address": "demartica 56/3",
          "created_at": "2021-10-28T14:45:27.000000Z",
          "updated_at": "2021-10-28T14:45:27.000000Z"
        },
        {
          "id": 542,
          "name": "Test",
          "last_name": "Test",
          "phone_number": "982379486",
          "email": "marekw1996@gmail.com",
          "country": "Polska",
          "city": "Szczecin",
          "address": "Test",
          "created_at": "2021-10-28T14:12:54.000000Z",
          "updated_at": "2021-10-28T14:12:54.000000Z"
        },
        {
          "id": 541,
          "name": "Alina",
          "last_name": "Kowalska",
          "phone_number": "945.468.9436",
          "email": "alina.kowalska19@gmail.com",
          "country": "Poland",
          "city": "Gdansk",
          "address": "80-547 Gdańsk, Władysława IV 13B 58 737-66-30, 737-66-62",
          "created_at": "2021-10-28T12:38:14.000000Z",
          "updated_at": "2021-10-28T12:38:14.000000Z"
        },
        {
          "id": 540,
          "name": "Jan",
          "last_name": "Kowalski",
          "phone_number": "945.458.9236",
          "email": "jan.kowalski23@gmail.com",
          "country": "Poland",
          "city": "Gdansk",
          "address": "80-547 Gdańsk, Władysława IV 13B 58 737-66-30, 737-66-62",
          "created_at": "2021-10-28T12:37:03.000000Z",
          "updated_at": "2021-10-28T12:37:03.000000Z"
        },
        {
          "id": 538,
          "name": "Krystel",
          "last_name": "Osinski",
          "phone_number": "940.438.9136",
          "email": "lemke.reese@gmail.com",
          "country": "Poland",
          "city": "Warsaw",
          "address": "2757 Rippin Gardens Apt. 010Aufderharfurt, TX 81917",
          "created_at": "2021-10-28T07:41:22.000000Z",
          "updated_at": "2021-10-28T07:41:22.000000Z"
        },
        {
          "id": 537,
          "name": "Krystel",
          "last_name": "Osinski",
          "phone_number": "940.438.9136",
          "email": "lemke.reese@gmail.com",
          "country": "Poland",
          "city": "Warsaw",
          "address": "2757 Rippin Gardens Apt. 010Aufderharfurt, TX 81917",
          "created_at": "2021-10-28T07:37:22.000000Z",
          "updated_at": "2021-10-28T07:37:22.000000Z"
        },
        {
          "id": 536,
          "name": "Krystel",
          "last_name": "Osinski",
          "phone_number": "940.438.9136",
          "email": "lemke.reese@gmail.com",
          "country": "Poland",
          "city": "Warsaw",
          "address": "2757 Rippin Gardens Apt. 010Aufderharfurt, TX 81917",
          "created_at": "2021-10-27T15:05:15.000000Z",
          "updated_at": "2021-10-27T15:05:15.000000Z"
        },
        {
          "id": 535,
          "name": "Krystel",
          "last_name": "Osinski",
          "phone_number": "940.438.9136",
          "email": "lemke.reese@gmail.com",
          "country": "Poland",
          "city": "Warsaw",
          "address": "2757 Rippin Gardens Apt. 010Aufderharfurt, TX 81917",
          "created_at": "2021-10-27T15:05:14.000000Z",
          "updated_at": "2021-10-27T15:05:14.000000Z"
        }
      ]
    }
  }
}
</script>
