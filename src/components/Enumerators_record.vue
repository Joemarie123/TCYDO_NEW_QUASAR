Marjorie Limsan
<template>
  <div>
    <div class="row">
      <!-- First Table (Left Side) -->
      <div class="col-3">
        <div class="col-12 col-sm-6 col-md-3 col-lg-9 q-mt-sm">
          <q-card class="my-card" bordered>
            <div class="row justify-center">
              
      <div class="header-container">
        <center>
        <h6 class="header"><b>Registered online list </b></h6>
      </center>
      </div>

              <div class="row d-flex justify-center">
                <div class="col-12 text-center">
                  <q-input outlined v-model="searchQuery" label="Search" @keyup.enter="search" class="search-input"></q-input>
                </div>
              </div>
            </div>
             
            <!-- Adjusted border style here -->
            <q-table class="my-sticky-dynamic" flat bordered :filter="filter" :rows="enumeratorRecords" :columns="columns"
              :loading="loading" row-key="index" virtual-scroll :virtual-scroll-item-size="48"
              :virtual-scroll-sticky-size-start="48" :pagination="pagination" :rows-per-page-options="[0]"
              @virtual-scroll="onScroll" style="max-width: 299px; border: 2px solid #ccc;">
              <template v-slot:body-cell-actions>
                <div class="actionsbtn">
                  <q-btn icon="edit" flat round color="secondary" @click="editItem"></q-btn>
                  <q-btn icon="delete" flat round color="deep-orange" @click="deleteItem"></q-btn>
                  <q-btn icon="security" flat round color="primary" @click="accessItem"></q-btn>
                </div>
              </template>
            </q-table>
          </q-card>
        </div>
      </div>
      
<!-- Second Table (Right Side) -->
<div class="col-9">
  <q-card class="my-card" bordered style="border-radius: 0px;">
    <div class="header-container">
      <div class="row">
        <div class="col-md-10">
          <h6 class="header"><b>To do List <br> 10 </b></h6>
        </div>
        <div class="col-md-2 text-center"> <!-- Column for search input -->
  <q-input outlined v-model="searchQuery" label="Search" @keyup.enter="search" class="search-input" style="border-color: white;"></q-input>
</div>
      </div>
    </div>
    <q-table class="my-sticky-dynamic" flat bordered :filter="filter" :rows="toDoList" :columns="toDoColumns"
      :loading="loading" row-key="index" virtual-scroll :virtual-scroll-item-size="48"
      :virtual-scroll-sticky-size-start="48" :pagination="pagination" :rows-per-page-options="[0]"
      @virtual-scroll="onScroll" style="max-width: 890px; border: 1px solid #ccc; border-radius: 0px;">
    </q-table>
  </q-card>
</div>





    </div>
  </div>
</template>

<style>
.header-container {
    background-color: #0c60fc;
    padding: 10px;
    margin-bottom: 20px;
    font-style: italic;
  }
  
  .header {
    color: rgb(255, 255, 255);
    margin: 0;
  };
  .rounded {
  border-radius: 20px; /* Adjust the value to change the roundness */
}

 
</style>

<script>
import { defineComponent } from "vue";
import { ref } from "vue";

export default defineComponent({
  name: "App",

  data() {
    return {
      filter: "",
      record: "",
      model: ref(null),
      columns: [
        {
          name: "record",
          required: true,
          label: "Enumerator's Record",
          align: "left",
          field: "record",
          format: (val) => val,
          sortable: true,
          width: "150px", // Adjust the width as needed
        },
      ],
      toDoColumns: [
        {
          name: "record",
          required: true,
          label: "Full Name",
          align: "left",
          field: "record",
          format: (val) => val,
          sortable: true,
          width: "150px", // Adjust the width as needed
        },
        {
          name: "email",
          required: true,
          label: "Email",
          align: "left",
          field: "email",
          format: (val) => val,
          sortable: true,
          width: "150px", // Adjust the width as needed
        },
        {
          name: "barangay_purok",
          required: true,
          label: "Barangay & Purok",
          align: "left",
          field: "barangay_purok",
          format: (val) => val,
          sortable: true,
          width: "150px", // Adjust the width as needed
        },
        {
          name: "date_survey",
          required: true,
          label: "Date Survey",
          align: "left",
          field: "date_survey",
          format: (val) => val,
          sortable: true,
          width: "150px", // Adjust the width as needed
        },
        // Add more columns as needed
      ],
      enumeratorRecords: [
        {
          record: "Joemarie Rendon Doe",
        },
        {
          record: "John Doe Smith",
        },
        // Additional rows to make the table longer
        {
          record: "Alice Johnson Doe",
        },
        {
          record: "Bob Williams Doe",
        },
        // Add more rows as needed
      ],
      toDoList: [
        // Define items for the To-Do List with full names and additional properties
        {
          record: "Alice Johnson Doe",
          email: "alice@example.com",
          barangay_purok: "Barangay 1, Purok 1",
          date_survey: "2024-04-05",
          // Add other properties for tasks
        },
        {
          record: "Bob Williams Doe",
          email: "bob@example.com",
          barangay_purok: "Barangay 2, Purok 2",
          date_survey: "2024-04-06",
          // Add other properties for tasks
        },
        {
          record: "Alice Johnson Doe",
          email: "alice@example.com",
          barangay_purok: "Barangay 1, Purok 1",
          date_survey: "2024-04-05",
          // Add other properties for tasks
        },
        {
          record: "Alice Johnson Doe",
          email: "alice@example.com",
          barangay_purok: "Barangay 1, Purok 1",
          date_survey: "2024-04-05",
          // Add other properties for tasks
        },
        {
          record: "Alice Johnson Doe",
          email: "alice@example.com",
          barangay_purok: "Barangay 1, Purok 1",
          date_survey: "2024-04-05",
          // Add other properties for tasks
        },
        {
          record: "Alice Johnson Doe",
          email: "alice@example.com",
          barangay_purok: "Barangay 1, Purok 1",
          date_survey: "2024-04-05",
          // Add other properties for tasks
        },
        {
          record: "Alice Johnson Doe",
          email: "alice@example.com",
          barangay_purok: "Barangay 1, Purok 1",
          date_survey: "2024-04-05",
          // Add other properties for tasks
        },
       

        // Add more tasks as needed
      ],
      searchQuery: "", // Added search query data property
    };
  },

  methods: {
    openFileInput() {
      this.$refs.fileInput.click();
    },
    handleFileChange(event) {
      const file = event.target.files[0];
      if (file) {
        this.imageUrl = null;
        this.imageUrl = URL.createObjectURL(file);
        this.$emit("image-selected", this.imageUrl);
      }
    },
    Rowclick() {
      this.dialogpersonal = true;
    },
    saveAndAddToTable() {
      // Save logic here for To-Do List
      this.toDoList.push({
        // Define the new item for the To-Do List
      });
      this.dialogpersonal = false; // Close dialog after saving
    },
    search() {
      // Search logic here
      console.log("Searching for:", this.searchQuery);
    },
  },
});

</script>