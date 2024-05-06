<template>
 
  <div class="header-container">
    <h4 class="header"><b>Registered Online List</b></h4>
   </div>



      <q-card class="my-card" bordered>
    <div class="col-10 row justify-start">
      <b><i><p style="font-size: 20px; color: #0c0c0c">Online List<br>registered list</p></i></b>
      <div class="col-10 row justify-end">
        <q-input class="search-input" borderless dense debounce="300" v-model="filter" placeholder="Search">
          <template v-slot:append>
            <q-icon name="search" />
          </template>
        </q-input>
      </div>
    </div>
      </q-card>

<br>

          
            
    <q-table
            :rows="formattedSeed"
            :columns="columns"
            row-key="index"
            :pagination="pagination"
            :rows-per-page-options="[0]"
          >
          </q-table>
       
  </template>
  
  
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
  
 .container {
display: flex;
flex-direction: column;
align-items: center;
height: 100vh;
}

.header-container {
background-color: #228B22;
margin: 3%;
padding: 10px;
margin-bottom: 20px;
}

.header {
color: white;
margin: 0;
}

.my-card, .my-table {
width: 100%;
}

.my-card {
box-shadow: 0px 10px 20px rgba(0, 0, 0, 0.2);
display: flex;
flex-direction: column;
flex-grow: 1; /* Fill available vertical space */

margin: 3%;
display: flex;
  flex-direction: column;
}

  .my-table {
background-color: #f0f0f0; /* Adjust as needed */
  }
  </style>
  