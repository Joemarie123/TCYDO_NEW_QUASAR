arjorie
Marjorie Limsan
<template>
  <div>
    <div class="row">
      <!-- First Table (Left Side) -->
      <div class="col-4">
        <div class="col-12 col-sm-6 col-md-3 col-lg-9 q-mt-sm">
          <q-card class="my-card" bordered>
            <q-banner class="bg-blue-6 text-white"> <!-- Changed bg-blue-6 to match the color of the header in the second table -->
              <center><p style="font-weight: bold; font-size: 20px;">Enumerator's Record</p></center> <!-- Adjusted font style -->
            </q-banner>
            <div class="row justify-center">
              <div class="header-container">
                <!-- <center>
                  <h6 class="header"><b>Registered online list </b></h6>
                </center> -->
              </div>
              <div class="col-md-2 text-center" style="width: 100%;"> <!-- Column for search input -->
                <q-input outlined v-model="searchQuery1" label="Search" @keyup.enter="search1" class="search-input" style="border-color: white; width: 100%;"></q-input>
              </div>
            </div>
            <!-- Adjusted border style here -->
            <q-table class="my-sticky-dynamic" flat bordered :filter="filter" :rows="enumeratorRecords" :columns="columns1"
                     :loading="loading" row-key="index" virtual-scroll :virtual-scroll-item-size="48"
                     :virtual-scroll-sticky-size-start="48" :pagination="pagination" :rows-per-page-options="[0]"
                     @virtual-scroll="onScroll" style="max-width: 360px; border: 2px solid #ccc;">
              <!-- Add a button column for Record List -->
              <template v-slot:body-cell-record-list-button="scope">
                <q-td :props="scope.props">
                  <q-btn flat color="primary" @click="recordList(scope.row)">Record List</q-btn>
                </q-td>
              </template>
              <!-- Adjust the alignment of the name and the record button -->
              <template v-slot:body-cell="scope">
                <q-td :props="scope.props">
                  <div class="q-td-content row justify-between">
                    <div class="col-auto">
                      {{ scope.row.record }}
                    </div>
                    <div class="col-auto">
                      <q-btn flat color="primary" @click="recordList(scope.row)" class="record-list-button">Record List</q-btn>
                    </div>
                  </div>
                </q-td>
              </template>
            </q-table>
          </q-card>
        </div>
      </div>
      <!-- Second Table (Right Side) -->
      <div class="col-8">
        <q-card class="my-card" bordered style="border-radius: 3px;">
          <q-banner class="bg-blue-6 text-white" style="justify-content: space-between;"> <!-- Changed bg-blue-6 to match the color of the header in the second table -->
            <div class="row align-items-center">
              <div class="col-md-auto">
                <p style="font-weight: bold; font-size: 20px;">Total Youth <br>10</p> <!-- Adjusted font style -->
              </div>
              <div class="col-md-auto q-ml-lg" style="width: 40%;"> <!-- Adjusted search bar alignment to the right -->
                <q-input outlined v-model="searchQuery2" label="Search" @keyup.enter="search2" class="search-input" style="border-radius: 100px;"></q-input>
              </div>
            </div>
          </q-banner>
          <q-table class="my-sticky-dynamic" flat bordered :filter="filter" :rows="toDoList" :columns="toDoColumns"
                   :loading="loading" row-key="index" virtual-scroll :virtual-scroll-item-size="48"
                   :virtual-scroll-sticky-size-start="48" :pagination="pagination" :rows-per-page-options="[0]"
                   @virtual-scroll="onScroll" style="max-width: 890px; border: 1px solid #ccc; border-radius: 0px;">
            <!-- Add a button column for Record List -->
            <template v-slot:body-cell-record-list-button="scope">
              <q-btn flat color="primary" @click="recordList(scope.row)">Record List</q-btn>
            </template>
          </q-table>
        </q-card>
      </div>
    </div>
  </div>
</template>

<style>
  .header-container { 
    background-color: #0c60fc;
    padding: 5px;
    margin-bottom: 10px;
  }
  .header {
    color: rgb(255, 255, 255);
    margin: 0;
  }
  .record-list-button {
    border: 1px solid yellowgreen;
    color: white; /* Change font color to white */
    background-color: lightgreen;
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
      columns1: [ 
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
      searchQuery1: "", // Added search query data property for Table 1
      searchQuery2: "", // Added search query data property for Table 2
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
    search1() {
      // Search logic here for Table 1
      console.log("Searching for Table 1:", this.searchQuery1);
    },
    search2() {
      // Search logic here for Table 2
      console.log("Searching for Table 2:", this.searchQuery2);
    },
    recordList(scope) {
      // Function to handle Record List button click inside the table
      console.log("Record List clicked:", scope.row.record);
      // You can perform actions related to the Record List button here
    },
  },
});
</script>