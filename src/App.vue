<template>
  <v-app id="inspire">
    <Form :dialog="dialogOpen" :editedContact="JSON.stringify(editContact)" @close="closeDialog" @reload="initialize"></Form>

    <v-app-bar app>
      <v-toolbar-title>Contacts</v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn text class="primary"
             @click="newContact">Add new contact
      </v-btn>
    </v-app-bar>

    <v-main>
      <Table @editItem="editItem" @reload="initialize" @options="options" :data="contacts" :total="total" :loading="loading"></Table>
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
      loading: true,
      dialogOpen: false,
      contacts: [],
      total: 0,
      page: 1,
      per_page: 10,
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
    options(payload) {
      this.page = payload.page;
      this.per_page = payload.per_page;
      this.initialize();
    },
    async initialize() {
      this.loading = true;
      this.contacts = [];
      let url = process.env.VUE_APP_API_URL;
      let urlPaginate = `${url}?per_page=${this.per_page}&page=${this.page}`;
      try {
        if (this.per_page === -1) {
          urlPaginate = `${url}?per_page=${this.total}&page=${this.page}`;
        }
        const res = await this.axios.get(urlPaginate);
        const { data, total } = res.data;
        this.contacts = data;
        this.total = total;
        this.loading = false;
      } catch (e) {
        console.log(e);
      }
    }
  }
}
</script>
