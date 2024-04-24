<template>
    <div>
      <div>
        <q-card class="my-card" bordered>
          <!-- Header Section -->
          <div class="row justify-start">
            <div class="col-3 col-sm-1 col-lg-1 q-pa-lg q-ml-lg">
              <img src="panda.jpg" alt="User Image" style="width: 40px; height: 40px; border-radius: 50%;">
            </div>
            <div class="col-5 col-sm-3 col-lg-2 q-pa-lg q-mt-sm text-center">
              <b><p style="font-size: 15px; color: #0c0c0c; display: inline-block;">User Account List</p></b>
            </div>
            <div class="col-10 col-sm-3 col-lg-5 q-pa-lg q-ml-lg text-center">
              <q-input v-model="filter" placeholder="Search">
                <template v-slot:append>
                  <q-icon name="search" />
                </template>
              </q-input>
            </div>
            <div class="col-12 col-sm-3 col-lg-3 q-pa-lg q-ml-lg">
              <q-btn
    icon="camera_enhance"
    glossy
    color="secondary"
    label="Create User Account"
    @click="Rowclick"
    :disabled="isFormIncomplete"
  />
  
            </div>
          </div>
  
          <!-- User Account Dialog -->
          <q-dialog v-model="dialogpersonal" persistent>
        <q-card :class="{ 'smaller-card': dialogMode === 'edit', 'wider-card': dialogMode === 'create' }"> <!-- Apply classes conditionally -->
          <q-card-section>
            <div class="text-h6">{{ dialogMode === 'create' ? 'Create User Account' : 'Edit Profile' }}</div>
          </q-card-section>
          <q-separator />
  
  <div class="col-12 q-pa-sm">
    <q-input filled label="First Name" v-model="newUser.firstName" dense class="q-pa-sm" />
    <q-input filled label="Middle Name" v-model="newUser.middleName" dense class="q-pa-sm" />
    <q-input filled label="Last Name" v-model="newUser.lastName" dense class="q-pa-sm" />
    <q-input filled label="Username" v-model="newUser.username" dense class="q-pa-sm" />
    <q-select filled label="User Level" v-model="newUser.userLevel" dense class="q-pa-sm" :options="userLevelOptions" />
    <q-select filled label="Barangay" v-model="newUser.barangay" dense class="q-pa-sm" :options="barangayOptions" />
  
    <!-- Show Password and Confirm Password fields only when creating a new user -->
    <template v-if="dialogMode === 'create'">
      <q-input filled label="Password" v-model="newUser.password" dense class="q-pa-sm" type="password" />
      <q-input filled label="Confirm Password" v-model="newUser.confirmPassword" dense class="q-pa-sm" type="password" />
    </template>
  </div>
  
  
              <!-- Save and Close Buttons -->
              <q-card-actions align="right">
            <q-btn label="Save" color="secondary" size="md" @click="saveAndAddToTable" />
            <q-btn flat label="Close" color="primary" v-close-popup size="md" />
          </q-card-actions>
        </q-card>
      </q-dialog>
  
          <!-- Table Component -->
          <q-table
            class="my-sticky-dynamic"
            flat
            bordered
            :filter="filter"
            :rows="seed"
            :columns="columns"
            :loading="loading"
            row-key="index"
            virtual-scroll
            :virtual-scroll-item-size="48"
            :virtual-scroll-sticky-size-start="48"
            :pagination="pagination"
            :rows-per-page-options="[0]"
            @virtual-scroll="onScroll"
          >
            <template v-slot:body-cell-actions="{ row }">
              <div class="actionsbtn">
                <q-btn icon="edit" flat round color="secondary" size="sm" class="smaller-btn" @click="editItem(row)"></q-btn>
                <div>
                  <q-toggle v-model="row.toggled" />
                </div>
              </div>
            </template>
          </q-table>
        </q-card>
      </div>
    </div>
  </template>
  
  <script>
  import { defineComponent } from "vue";
  
  export default defineComponent({
    name: "App",
  
    data() {
    return {
      dialogpersonal: false,
      dialogMode: 'create',
        newUser: {
          username: "",
          firstName: "",
          middleName: "",
          lastName: "",
          userLevel: "",
          barangay: "",
          password: "",
          confirmPassword: "",
        },
        userLevelOptions: ["Admin", "Brgy. SK Official", "Youth Enumerator"],
        barangayOptions: ["Apokon", "Bincungan", "Busaon", "Canocotan", "Cuambogan", "La Filipina", "Liboganon", "Madaum", "Magdum", "Mankilam", "New Balamban", "Nueva Fuerza", "Pagsabangan", "Pandapan", "Magugpo Poblacion", "San Agustin", "San Isidro", "San Miguel (Camp 4)", "Visayan Village", "Magugpo East", "Magugpo North", "Magugpo South", "Magugpo West"],
        columns: [
          { name: "firstName", label: "First Name", align: "left", field: "firstname", sortable: true },
          { name: "middleName", label: "Middle Name", align: "left", field: "middlename", sortable: true },
          { name: "lastName", label: "Last Name", align: "left", field: "lastname", sortable: true },
          { name: "username", label: "Username", align: "left", field: "username", sortable: true },
          { name: "userLevel", label: "User Level", align: "left", field: "userLevel" },
          { name: "barangay", label: "Barangay", align: "left", field: "barangay" },
          { name: "actions", label: "Actions", align: "left", field: "action" },
        ],
        seed: [
          { firstname: "Stephen", middlename: "Dela Cruz", lastname: "Curry", username: "steph23", userLevel: "Admin", barangay: "Apokon", toggled: false },
          { firstname: "Wony", middlename: "Santiago", lastname: "Jang", username: "wonysm16", userLevel: "Admin", barangay: "Apokon", toggled: false },
          { firstname: "Taylor", middlename: "Alison", lastname: "Swift", username: "taytay13", userLevel: "Admin", barangay: "Apokon", toggled: false },
        ],
        loading: false,
        pagination: { rowsPerPage: 5 },
        filter: "",
      };
    },
  
    methods: {
      Rowclick() {
        this.dialogMode = 'create';
        this.dialogpersonal = true;
        this.clearForm();
        this.dialogpersonal = true;
      },
      
      editItem(row) {
        // Set dialog mode to 'edit'
      this.dialogMode = 'edit';
  
  // Populate fields with row data
  this.newUser.firstName = row.firstname;
  this.newUser.middleName = row.middlename;
  this.newUser.lastName = row.lastname;
  this.newUser.username = row.username;
  this.newUser.userLevel = row.userLevel;
  this.newUser.barangay = row.barangay;
  
  // Open the dialog
  this.dialogpersonal = true;
      },
  
      clearForm() {
      // Clear all form fields in newUser object
      this.newUser.firstName = "";
      this.newUser.middleName = "";
      this.newUser.lastName = "";
      this.newUser.username = "";
      this.newUser.userLevel = "";
      this.newUser.barangay = "";
      this.newUser.password = "";
      this.newUser.confirmPassword = "";
    },
  
    saveAndAddToTable() {
    if (
      this.newUser.lastName &&
      this.newUser.firstName &&
      this.newUser.middleName &&
      this.newUser.username &&
      this.newUser.userLevel &&
      this.newUser.barangay
    ) {
      if (this.dialogMode === 'create') {
        // Check if passwords match
        if (this.newUser.password !== this.newUser.confirmPassword) {
          alert("Passwords do not match.");
          return;
        }
      }
  
      const newUser = {
        firstname: this.newUser.firstName,
        middlename: this.newUser.middleName,
        lastname: this.newUser.lastName,
        username: this.newUser.username,
        userLevel: this.newUser.userLevel,
        barangay: this.newUser.barangay,
      };
  
          // Push the new user object to the seed array
          this.seed.push(newUser);
  
          // Close dialog after saving
          this.dialogpersonal = false;
  
        } else {
          // Alert user to fill in all fields
          alert("Please fill in all fields.");
        }
      },
  
      computed: {
    isFormIncomplete() {
      const { firstName, middleName, lastName, username, userLevel, barangay } = this.newUser;
      return !firstName || !middleName || !lastName || !username || !userLevel || !barangay;
    }
  },
  
  
    },
  });
  </script>
  
  <style scoped>
  .my-card {
    box-shadow: 0px 10px 20px rgba(0, 0, 0, 0.2);
    margin: 3%;
    display: flex;
    flex-direction: column;
    height: 100%;
  }
  
  .smaller-card {
    width: 40%; /* Adjust width as needed for the Edit Profile dialog */
    height: 60%; /* Adjust height as needed for the Edit Profile dialog */
  }
  
  .wider-card {
    width: 60%; /* Adjust width as needed for the Create User Account dialog */
    height: 75%; /* Adjust height as needed for the Create User Account dialog */
  }
  </style>
  