<template>
  <div class="q-pa-sm">
    <q-card>
      <q-card-section class="header-container">
        <div style="display: flex; justify-content: space-between; align-items: center;">
          <h4 class="header"><b>ALL YOUTH RECORD</b></h4>
          <div style="display: flex; align-items: center;">
            <q-input borderless dense debounce="300" v-model="filter" placeholder="Search" class="expanded-search">
              <template v-slot:append>
                <q-icon name="search" />
              </template>
            </q-input>
            <q-btn flat label="Print" @click="printData" />
          </div>
        </div>
      </q-card-section>

      <q-table :rows="filteredRows" :columns="columns" row-key="name">
        <template v-slot:body-cell-action="props">
          <q-td :props="props" :class="props.colClass">
            <div style="display: flex; align-items: center; justify-content: center;">
              <q-btn class="q-mx-md" color="primary" label="Event History" @click="showEventHistory(props.row)"></q-btn>
              <q-btn color="secondary" label="View Profile" @click="showDialog(props.row)"></q-btn>
            </div>
          </q-td>
        </template>
      </q-table>
    </q-card>

    <q-dialog v-model="showDialogDialog">
      <q-card>
        <q-card-section class="profile-info-container">
          <h5><b>User Information</b></h5>
        </q-card-section>

        <q-card-section class="profile-info-inside">
          <div class="profile-info-row">
            <q-item-label class="profile-info-label"><b>Name:</b></q-item-label>
            <q-item-label class="profile-info-value">{{ userData.name }}</q-item-label>
          </div>

          <div class="profile-info-row">
            <q-item-label class="profile-info-label"><b>Email:</b></q-item-label>
            <q-item-label class="profile-info-value">{{ userData.email }}</q-item-label>
          </div>

          <div class="profile-info-row">
            <q-item-label class="profile-info-label"><b>Mobile Number:</b></q-item-label>
            <q-item-label class="profile-info-value">{{ userData.mobile }}</q-item-label>
          </div>

          <div class="profile-info-row">
            <q-item-label class="profile-info-label"><b>Barangay & Purok:</b></q-item-label>
            <q-item-label class="profile-info-value">{{ userData.barangay }}</q-item-label>
          </div>

          <div class="profile-info-row">
            <q-item-label class="profile-info-label"><b>Birthday:</b></q-item-label>
            <q-item-label class="profile-info-value">{{ userData.birthday }}</q-item-label>
          </div>

          <div class="profile-info-row">
            <q-item-label class="profile-info-label"><b>Age:</b></q-item-label>
            <q-item-label class="profile-info-value">{{ userData.age }}</q-item-label>
          </div>

          <div class="profile-info-row">
            <q-item-label class="profile-info-label"><b>Voters:</b></q-item-label>
            <q-item-label class="profile-info-value">{{ userData.voters }}</q-item-label>
          </div>

          <div class="profile-info-row">
            <q-item-label class="profile-info-label"><b>Ethics:</b></q-item-label>
            <q-item-label class="profile-info-value">{{ userData.ethics }}</q-item-label>
          </div>

          <div class="profile-info-row">
            <q-item-label class="profile-info-label"><b>Education:</b></q-item-label>
            <q-item-label class="profile-info-value">{{ userData.education }}</q-item-label>
          </div>

          <div class="profile-info-row">
            <q-item-label class="profile-info-label"><b>Data Survey:</b></q-item-label>
            <q-item-label class="profile-info-value">{{ userData.dataSurvey }}</q-item-label>
          </div>

          <div class="profile-info-row">
            <q-item-label class="profile-info-label"><b>Civil Status:</b></q-item-label>
            <q-item-label class="profile-info-value">{{ userData.civilStatus }}</q-item-label>
          </div>

          <div class="profile-info-row">
            <q-item-label class="profile-info-label"><b>Gender:</b></q-item-label>
            <q-item-label class="profile-info-value">{{ userData.gender }}</q-item-label>
          </div>

          <div class="profile-info-row">
            <q-item-label class="profile-info-label"><b>Active Status:</b></q-item-label>
            <q-item-label class="profile-info-value">{{ userData.activeStatus }}</q-item-label>
          </div>
        </q-card-section>

        <q-card-actions align="left">
          <q-btn label="Edit Profile" color="primary" @click="showEditProfileDialog = true"></q-btn>
          <q-btn label="Block" color="red" @click="blockUser"></q-btn>
          <q-btn label="Close" @click="showDialogDialog = false"></q-btn>
        </q-card-actions>
      </q-card>
    </q-dialog>

    <q-dialog v-model="showEditProfileDialog">
      <q-card>
        <q-card-section class="edit-profile-section">
          <h5><b>Edit Profile</b></h5>
          <q-item>
            <q-item-label><b>Name:</b></q-item-label>
            <q-item-label>
              <q-input v-model="editedName" dense />
            </q-item-label>
          </q-item>
          <q-item>
            <q-item-label><b>Email:</b></q-item-label>
            <q-item-label>
              <q-input v-model="userData.email" dense />
            </q-item-label>
          </q-item>
          <q-item>
            <q-item-label><b>Mobile Number:</b></q-item-label>
            <q-item-label>
              <q-input v-model="userData.mobile" dense />
            </q-item-label>
          </q-item>
          <q-item>
            <q-item-label><b>Barangay & Purok:</b></q-item-label>
            <q-item-label>
              <q-input v-model="userData.barangay" dense />
            </q-item-label>
          </q-item>
          <q-item>
            <q-item-label><b>Birthday:</b></q-item-label>
            <q-item-label>
              <q-input v-model="userData.birthday" dense />
            </q-item-label>
          </q-item>
          <q-item>
            <q-item-label><b>Gender:</b></q-item-label>
            <q-item-label>
              <q-input v-model="userData.gender" dense />
            </q-item-label>
          </q-item>
          <q-item>
            <q-item-label><b>Civil Status:</b></q-item-label>
            <q-item-label>
              <q-input v-model="userData.civilStatus" dense />
            </q-item-label>
          </q-item>
        </q-card-section>

        <q-card-actions align="right">
          <q-btn label="Save Changes" color="primary" @click="saveChanges"></q-btn>
          <q-btn label="Cancel" @click="showEditProfileDialog = false"></q-btn>
        </q-card-actions>
      </q-card>
    </q-dialog>

    <q-dialog v-model="showEventHistoryDialog">
      <q-card>
        <q-card-section>
          <div style="display: flex; justify-content: space-between; align-items: center;">
            <q-input borderless dense debounce="300" v-model="eventFilter" placeholder="Search Events" class="expanded-search" />
            <q-btn flat label="Close" @click="showEventHistoryDialog = false" class="close-button" />
          </div>
          <q-table :rows="filteredEventRows" :columns="eventColumns" row-key="id">
            <template v-slot:body="props">
              <q-tr :props="props">
                <q-td key="name" :props="props" :class="props.colClass">
                  <div style="display: flex; align-items: center;">
                    {{ props.row.name }}
                  </div>
                </q-td>
                <q-td key="date" :props="props" :class="props.colClass">{{ props.row.date }}</q-td>
                <q-td key="details" :props="props" :class="props.colClass">{{ props.row.details }}</q-td>
                <q-td key="hoursEarned" :props="props" :class="props.colClass" align="center">{{ props.row.hoursEarned }}</q-td>
              </q-tr>
            </template>
          </q-table>
        </q-card-section>
      </q-card>
    </q-dialog>
  </div>
</template>

<script>
import { ref, computed } from 'vue';

export default {
  setup() {
    const showDialogDialog = ref(false);
    const showEditProfileDialog = ref(false);
    const showEventHistoryDialog = ref(false);
    const userData = ref({
      name: '',
      email: '',
      mobile: '',
      barangay: '',
      birthday: '',
      age: '',
      voters: '',
      ethics: '',
      education: '',
      dataSurvey: '',
      civilStatus: '',
      gender: '',
      activeStatus: '',
    });

    const editedName = ref('');

    const filter = ref('');
    const eventFilter = ref('');

    const columns = [
      { name: 'name', label: 'Full Name', field: 'name', align: 'left', sortable: true },
      { name: 'email', label: 'Email', field: 'email', align: 'left', sortable: true },
      { name: 'mobile', label: 'Mobile Number', field: 'mobile', align: 'left', sortable: true },
      { name: 'barangay', label: 'Barangay & Purok', field: 'barangay', align: 'left', sortable: true },
      { name: 'action', label: 'Action', align: 'center', sortable: false },
    ];

    const eventColumns = [
      { name: 'name', label: 'Event Name', field: 'name', align: 'left', sortable: true, style: 'width: 300px;' },
      { name: 'date', label: 'Date', field: 'date', align: 'left', sortable: true, style: 'width: 150px;' },
      { name: 'details', label: 'Details', field: 'details', align: 'left', sortable: true, style: 'width: 500px;' },
      { name: 'hoursEarned', label: 'Hours Earned', field: 'hoursEarned', align: 'center', sortable: true, style: 'width: 150px;' },
    ];

    const rows = ref([
      {
        name: 'Kyle a.k.a geng geng Viernes',
        email: 'kyleviernes16@gmail.com',
        mobile: '093284567879',
        barangay: 'Apokon - Purok 10',
        action: '',
        birthday: '1992-08-15',
        age: '32',
        voters: 'Yes',
        ethics: 'Good',
        education: 'College', 
        dataSurvey: 'Completed',
        civilStatus: 'Single',
        gender: 'Male',
        activeStatus: 'Active',
      },
      {
        name: 'Jann a.k.a TheSadboy Juson',
        email: 'jannjuson18@gmail.com',
        mobile: '09435997544',
        barangay: 'Apokon - Purok 9',
        action: '',
        birthday: '1995-05-15',
        voters: 'No',
        ethics: 'Neutral',
        education: 'High School',
        dataSurvey: 'Pending',
        civilStatus: 'Married',
        gender: 'Female',
        activeStatus: 'Inactive', 
      },
    ]);

    const eventHistoryData = ref([
      {
        name: 'Tagum Lighting of Christmas tree',
        date: 'December 4,2022',
        details: 'The tallest Christmas tree in the Philippines was illuminated on Wednesday night in Tagum City, Davao del Norte.',
        hoursEarned: 2
      },
      { id: 2, name: 'Event 2', date: '2024-04-15', details: 'Details for Event 2', hoursEarned: 3 },
    ]);

    const showDialog = (row) => {
      userData.value = { ...row }; 
      showDialogDialog.value = true;
    };

    const saveChanges = () => {
      userData.value.name = editedName.value;  
      console.log('Changes saved!');
      showEditProfileDialog.value = false;
    };

    const blockUser = () => {
      console.log('User blocked!');
    };

    const handleButtonClick = (event) => {
      console.log('Button clicked for event:', event);
    };

    const filteredRows = computed(() => {
      return rows.value.filter(row => {
        return row.name.toLowerCase().includes(filter.value.toLowerCase());
      });
    });

    const printData = () => {
      console.log('PRINT');
    };

    const showEventHistory = (row) => {
      showEventHistoryDialog.value = true;
    };

    const handleEventClick = (event) => {
      console.log('Event clicked:', event);
    };

    const filteredEventRows = computed(() => {
      return eventHistoryData.value.filter(event => {
        return event.name.toLowerCase().includes(eventFilter.value.toLowerCase());
      });
    });

    return {
      showDialogDialog,
      showEditProfileDialog,
      showEventHistoryDialog,
      userData,
      editedName,
      filter,
      eventFilter,
      columns,
      eventColumns,
      rows,
      eventHistoryData,
      showDialog,
      saveChanges,
      blockUser,
      handleButtonClick,
      filteredRows,
      filteredEventRows,
      printData,
      showEventHistory,
      handleEventClick,
    };
  },
};
</script>

<style scoped>
.q-dialog .q-card {
  width: 80%;
}

.profile-info-inside {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
}

.header-container {
  margin-bottom: 20px;
}

.header {
  color: rgb(9, 9, 9);
  margin: 0;
}

.profile-info-label {
  min-width: 150px;
  margin-right: 10px;
  font-weight: bold;
  color: #333;
}

.profile-info-value {
  flex: 1;
  color: #666;
}

.edit-profile-section {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.profile-info-container {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.profile-info-row {
  display: flex;
  align-items: center;
  margin-left: 10px;
}

.profile-info-label {
  min-width: 300px;
  text-align: center;
  flex-basis: 30%;
}

.rounded-input .q-field__native {
  border-radius: 20px;
}

.expanded-search .q-field__native {
  width: 300px;
}

.add-button-column {
  display: flex;
  align-items: center;
  justify-content: flex-end;
  margin-top: 20px;
}

.close-button {
  margin-left: 10px;
}
</style>