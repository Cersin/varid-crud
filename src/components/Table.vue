<template>
  <v-data-table
      :headers="headers"
      :items="data"
      class="elevation-1"
      :loading="loading"
      :server-items-length="total"
      :options.sync="options"
      @update:page="paginate"
  >
    <template v-slot:top>
      <v-toolbar
          flat
      >
        <v-toolbar-title>Varid Table</v-toolbar-title>

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
          @click="$emit('editItem', item)"
      >
        mdi-pencil
      </v-icon>
      <v-icon
          small
          @click="$emit('deleteItem', item)"
      >
        mdi-delete
      </v-icon>
    </template>
  </v-data-table>
</template>

<script>

export default {
  props: ['data', 'loading', 'total'],
  data: () => ({
    options: {},
    dialogOpen: false,
    dialogDelete: false,
    editContact: null,
    headers: [
      {
        text: 'Name',
        align: 'start',
        sortable: false,
        value: 'name',
      },
      {text: 'Last Name', value: 'last_name'},
      {text: 'Phone', value: 'phone_number'},
      {text: 'Email', value: 'email'},
      {text: 'Country', value: 'country'},
      {text: 'City', value: 'city'},
      {text: 'Address', value: 'address'},
      {text: 'Actions', value: 'actions', sortable: false}
    ]
  }),
  methods: {
    paginate() {
      this.$emit('options', {
        page: this.options.page,
        per_page: this.options.itemsPerPage
      });
    }
  }
}
</script>

<style scoped>

</style>
