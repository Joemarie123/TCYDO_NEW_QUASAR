<template>

    <h5><b>Registered Online List</b></h5>
    
    
    
    
      <div class="q-pa-md">
            
            
    
        
        <div class="header-lang">
             <center>
            <h3 class="header"><b> &nbsp; </b></h3>
          </center>
          </div>
    
          
          <div class="col-12 col-sm-6 col-md-3 col-lg-9 q-mt-sm">
            <q-card class="my-card" bordered>
              <div class="row justify-start">
                <div class="col-2 q-pa-md">
                <b><i><p style="font-size: 20px; color: #0c0c0c">Online List<br>huieeeee</p></i></b>
                </div>   
      
                <q-dialog v-model="dialogpersonal" persistent>x
                  <q-card style="width: 50%; height: 75%">
                    <q-card-section>
                      <div class="text-h6" align="center">Create Events</div>
                    </q-card-section>
      
                    <q-separator />
      
                    <div class="row q-pa-sm">
                      <div class="col-12">
                        <q-input filled label="Full Name" v-model="fullName" dense class="q-pa-sm" />
                      </div>
                    </div>
      
                    <div class="row q-pa-sm">
                      <div class="col-6">
                        <q-input type="email" filled label="Email" v-model="email" dense class="q-pa-sm" />
                      </div>
                      <div class="col-6">
                        <q-input filled label="Barangay & Purok" v-model="barangayPurok" dense class="q-pa-sm" />
                      </div>
                    </div>
      
                    <div class="row q-pa-sm">
                      <div class="col-12">
                        <q-input filled label="Event Details" v-model="eventDetails" dense class="q-pa-sm" type="textarea" style="min-height: 100px;" />
                      </div>
                    </div>
      
                    <q-card-section style="max-height: 50vh" class="scroll">
                      <q-form>
                        <!-- Other input fields here -->
                      </q-form>
                    </q-card-section>
                    
                    <q-card-actions align="left">
                      <q-btn label="CONTINUE" color="primary" size="md" @click="saveAndAddToTable" />
                      <q-btn flat label="CLOSE" color="secondary" v-close-popup size="md" />
                    </q-card-actions>
                  </q-card>
                </q-dialog>
      
              
                <div class="col-4 q-pa-sm mx-auto search-container">
        <q-input class="search-input" borderless dense debounce="300" v-model="filter" placeholder="Search">
          <template v-slot:append>
            <q-icon name="search" />
          </template>
        </q-input>
      </div>
    
    
      
              </div>
              <q-table
                :rows="formattedSeed"
                :columns="columns"
                row-key="index"
                :pagination="pagination"
                :rows-per-page-options="[0]"
              >
              </q-table>
            </q-card>
          </div>
        </div>
      </template>
      
      <style>
        
      
      
    
      .header-lang {
        background-color: #5478b6;
        padding: 10px;
        margin-bottom: 20px;
        font-style: normal;
      }
      
      .header {
        color: rgb(255, 255, 255);
        margin: 0;
      }
      
      .search-container {
      border-radius: 50px; /* Adjust border radius as needed */
      overflow: show; /* Ensure the border-radius clips the content properly */
    }
    
    /* Style for the input itself */
    .search-input {
      width: 100%; /* Make the input fill its container */
    }
    
    
    
    
      </style>
      
      
      <script>
      import { defineComponent } from "vue";
      import { ref } from "vue";
      
      export default defineComponent({
        name: "App",
      
        data() {
          return {
            dialogpersonal: false,
            filter: "",
            fullName: "",
            email: "",
            barangayPurok: "",
            eventDetails: "",
            model: ref(null),
            columns: [
              {
                name: "fullName",
                align: "left",
                label: "Full Name",
                field: "fullName",
                sortable: true,
              },
              {
                name: "email",
                label: "Email",
                align: "left",
                field: "email",
                sortable: true,
              },
              {
                name: "barangayPurok",
                label: "Barangay & Purok",
                align: "left",
                field: "barangayPurok",
                sortable: true,
              },
              {
                name: "eventDetails",
                label: "Event Details",
                align: "left",
                field: "eventDetails",
                sortable: true,
              }
            ],
            seed: [
              {
                fullName: "Clarken Tubo",
                email: "bAbyCl4rk@waT4p4mpa.com",
                barangayPurok: "Apokon - Purok 1",
                eventDetails: "Details of Event 1",
              },
              {
                fullName: "James Rainier Junto",
                email: "Nicolai.Rin@yandex.com",
                barangayPurok: "Magugpo West - Purok 2",
                eventDetails: "Details of Event 2",
              },
              {
                fullName: "Michael Angelo Pendon",
                email: "MickeyMic@yandex.com",
                barangayPurok: "Liboganon - Purok 3",
                eventDetails: "Details of Event 3",
              },
              {
                fullName: "Ashley Liv Nacorda",
                email: "john.doe@example.com",
                barangayPurok: "Apokon - Purok 1",
                eventDetails: "Details of Event 1",
              },
              {
                fullName: "Lovemae Pamplona",
                email: "jane.smith@example.com",
                barangayPurok: "Magugpo West - Purok 2",
                eventDetails: "Details of Event 2",
              },
              {
                fullName: "Liz Angely Dayaon",
                email: "alice.johnson@example.com",
                barangayPurok: "Liboganon - Purok 3",
                eventDetails: "Details of Event 3",
              },
              {
                fullName: "Jane Smith",
                email: "jane.smith@example.com",
                barangayPurok: "Magugpo West - Purok 2",
                eventDetails: "Details of Event 2",
              },
              {
                fullName: "Jodell Binasbas",
                email: "alice.johnson@example.com",
                barangayPurok: "Liboganon - Purok 3",
                eventDetails: "Details of Event 3",
              },
              {
                fullName: "Rona Grace Cabanela",
                email: "jane.smith@example.com",
                barangayPurok: "Magugpo West - Purok 2",
                eventDetails: "Details of Event 2",
              },
              {
                fullName: "Elaine Mae Obregon",
                email: "alice.johnson@example.com",
                barangayPurok: "Liboganon - Purok 3",
                eventDetails: "Details of Event 3",
              },
              {
                fullName: "Gerald Marfe",
                email: "alice.johnson@example.com",
                barangayPurok: "Liboganon - Purok 3",
                eventDetails: "Details of Event 3",
              },
              {
                fullName: "Alrich Joanna Apit",
                email: "jane.smith@example.com",
                barangayPurok: "Magugpo West - Purok 2",
                eventDetails: "Details of Event 2",
              },
              {
                fullName: "Stacy Karol Isaabella Bigno",
                email: "alice.johnson@example.com",
                barangayPurok: "Liboganon - Purok 3",
                eventDetails: "Details of Event 3",
              },
              {
                fullName: "Rica Mae Vitor",
                email: "jane.smith@example.com",
                barangayPurok: "Magugpo West - Purok 2",
                eventDetails: "Details of Event 2",
              },
              {
                fullName: "Xious Sardoma",
                email: "alice.johnson@example.com",
                barangayPurok: "Liboganon - Purok 3",
                eventDetails: "Details of Event 3",
              },
              {
                fullName: "Cliiford Galamiton",
                email: "jane.smith@example.com",
                barangayPurok: "Magugpo West - Purok 2",
                eventDetails: "Details of Event 2",
              },
                    
            ],
            loading: false,
            pagination: { rowsPerPage: 18 },
          };
        },
      
        computed: {
          formattedSeed() {
            return this.seed.map(event => {
              return event;
            });
          },
        },
      
        methods: {
          Rowclick() {
            this.dialogpersonal = true;
          },
          saveAndAddToTable() {
            if (this.fullName && this.email && this.barangayPurok && this.eventDetails) {
              this.seed.push({
                fullName: this.fullName,
                email: this.email,
                barangayPurok: this.barangayPurok,
                eventDetails: this.eventDetails,
              });
              this.dialogpersonal = false;
              this.clearForm();
            } else {
              alert('Please fill in all fields.');
            }
            
          },
          clearForm() {
            this.fullName = "";
            this.email = "";
            this.barangayPurok = "";
            this.eventDetails = "";
          },
          
        },
      });
      </script>
      
      
      <style scoped>
      .my-card {
        box-shadow: 0px 10px 20px rgba(0, 0, 0, 0.2);
        margin: 1%;
        display: flex;
        flex-direction: column;
        height: 100%;
      }
      .q-table-container {
      background-color: #338edf; 
      }
      
      </style>
      