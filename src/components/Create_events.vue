<template>
  <div>
    <div class="col-12 col-sm-6 col-md-3 col-lg-9 q-mt-sm">
      <q-card class="my-card" bordered>
        <div class="row justify-start">
          <div class="col-2 q-pa-md">
            <!-- Picture with border-radius -->
            <img src="sadaadsa" alt="Event" style="border-radius: 100%; width: 100%;" />
          </div>
          <div class="col">
            <b>
              <p style="font-size: 20px; color: #0c0c0c; padding-top: 10px; font-weight: bold; white-space: nowrap;">
                Event List
              </p>
            </b>
          </div>

          <div class="col-4 q-pa-sm" style="padding-left: 150px;">
            <!-- Adjusted to the right -->
            <q-input borderless dense debounce="400" v-model="filter" placeholder="Search">
              <template v-slot:append>
                <q-icon name="search" />
              </template>
            </q-input>
          </div>

          <div class="col-6 q-pa-sm text-right">
            <q-btn icon="camera_enhance" glossy color="secondary" label="Create Event" @click="Rowclick" />
          </div>
        </div>
        <q-table
          :rows="formattedSeed"
          :columns="columns"
          row-key="index"
          :pagination="pagination"
          :rows-per-page-options="[0]"
        >
          <template v-slot:body-cell-actions="{ row }">
            <q-td :props="cellProps">
              <div class="q-gutter-xs row inline justify-end"> <!-- Adjusted to the right -->
                <q-btn
                  icon="edit"
                  flat
                  round
                  color="secondary"
                  @click="editItem(row)"
                />
                <q-btn
                  icon="delete"
                  flat
                  round
                  color="deep-orange"
                  @click="deleteItem(row)"
                />
              </div>
            </q-td>
          </template>
        </q-table>
      </q-card>
    </div>
  </div>
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
      eventName: "",
      eventDate: null,
      numParticipants: null,
      eventDetails: "",
      model: ref(null),
      columns: [
        {
          name: "eventName",
          align: "left",
          label: "Event Name",
          field: "eventName",
          sortable: true,
        },
        {
          name: "formattedEventDate",
          label: "Date",
          align: "left",
          field: "formattedEventDate",
          sortable: true,
        },
        {
          name: "eventDetails",
          label: "Event Details",
          align: "left",
          field: "eventDetails",
          sortable: true,
        },
        {
          name: "numParticipants",
          label: "Participants",
          align: "left",
          field: "numParticipants",
          sortable: true,
        },
        {
          name: "actions",
          label: "Actions",
          align: "center",
          field: "actions",
          format: (val, row) => "",
        },
      ],
      seed: [
        {
          eventName: "Event 1",
          eventDate: "2024-04-01",
          eventDetails: "Details of Event 1",
          numParticipants: 10,
        },
        {
          eventName: "Event 2",
          eventDate: "2024-04-15",
          eventDetails: "Details of Event 2",
          numParticipants: 20,
        },
        {
          eventName: "Event 3",
          eventDate: "2024-04-30",
          eventDetails: "Details of Event 3",
          numParticipants: 15,
        },
      ],
      loading: false,
      pagination: { rowsPerPage: 5 },
      editedItemIndex: null,
    };
  },

  computed: {
    formattedSeed() {
      return this.seed.map(event => ({
        ...event,
        formattedEventDate: this.formatDate(event.eventDate),
      }));
    },
  },

  methods: {
    Rowclick() {
      this.dialogpersonal = true;
      this.editedItemIndex = null;
    },
    saveAndAddToTable() {
      if (this.eventName && this.eventDate && this.eventDetails && this.numParticipants) {
        if (this.editedItemIndex !== null) {
          // If an item is being edited
          this.seed[this.editedItemIndex] = {
            eventName: this.eventName,
            eventDate: this.eventDate,
            eventDetails: this.eventDetails,
            numParticipants: this.numParticipants,
          };
          this.editedItemIndex = null;
        } else {
          // If a new item is being added
          this.seed.push({
            eventName: this.eventName,
            eventDate: this.eventDate,
            eventDetails: this.eventDetails,
            numParticipants: this.numParticipants,
          });
        }
        this.dialogpersonal = false;
        this.clearForm();
      } else {
        alert('Please fill in all fields.');
      }
    },
    clearForm() {
      this.eventName = "";
      this.eventDate = null;
      this.eventDetails = "";
      this.numParticipants = null;
    },
    editItem(row) {
      // Set the fields with the data of the selected row
      this.eventName = row.eventName;
      this.eventDate = row.eventDate;
      this.eventDetails = row.eventDetails;
      this.numParticipants = row.numParticipants;
      this.dialogpersonal = true;
      this.editedItemIndex = this.seed.indexOf(row);
    },
    deleteItem(row) {
      const index = this.seed.indexOf(row);
      if (index !== -1) {
        this.seed.splice(index, 1);
      }
    },
    formatDate(date) {
      const options = { year: 'numeric', month: 'long', day: 'numeric' };
      return new Date(date).toLocaleDateString(undefined, options);
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
</style>