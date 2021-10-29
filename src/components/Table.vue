<template>
  <v-data-table
      :headers="headers"
      :items="data"
      class="elevation-1"
      :items-per-page="perPage"
      :server-items-length="total"
      :options.sync="options"
  >
    <template v-slot:top>
      <v-toolbar
          flat
      >
        <v-toolbar-title>Varid CRUD</v-toolbar-title>
        <v-divider
            class="mx-4"
            inset
            vertical
        ></v-divider>
        <v-spacer></v-spacer>
        <Form></Form>
<!--        <v-dialog v-model="dialogDelete" max-width="500px">-->
<!--          <v-card>-->
<!--            <v-card-title class="text-h5">Are you sure you want to delete this item?</v-card-title>-->
<!--            <v-card-actions>-->
<!--              <v-spacer></v-spacer>-->
<!--              <v-btn color="blue darken-1" text @click="closeDelete">Cancel</v-btn>-->
<!--              <v-btn color="blue darken-1" text @click="deleteItemConfirm">OK</v-btn>-->
<!--              <v-spacer></v-spacer>-->
<!--            </v-card-actions>-->
<!--          </v-card>-->
<!--        </v-dialog>-->
      </v-toolbar>
    </template>
    <template v-slot:item.actions="{ item }">
      <v-icon
          small
          class="mr-2"
          @click="editItem(item)"
      >
        mdi-pencil
      </v-icon>
      <v-icon
          small
          @click="deleteItem(item)"
      >
        mdi-delete
      </v-icon>
    </template>
    <template v-slot:no-data>
      <v-btn
          color="primary"
          @click="initialize"
      >
        Reset
      </v-btn>
    </template>
  </v-data-table>
</template>

<script>
import Form from "@/components/Form";
export default {
  components: {Form},
  props: ['data'],
  data: () => ({
    dialog: false,
    dialogDelete: false,
    perPage: 5,
    total: 68,
    options: {
      page: 1,
      itemsPerPage: 10
    },
    headers: [
      {
        text: 'Name',
        align: 'start',
        sortable: false,
        value: 'name',
      },
      { text: 'Last Name', value: 'last_name' },
      { text: 'Phone', value: 'phone_number' },
      { text: 'Email', value: 'email' },
      { text: 'Country', value: 'country' },
      { text: 'City', value: 'city' },
      { text: 'Adress', value: 'address' },
      { text: 'Actions', value: 'actions', sortable: false }
    ],

    contacts: [],
  })
}
</script>

<style scoped>

</style>
