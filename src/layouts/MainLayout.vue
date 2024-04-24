<template>
  <q-layout view="lHh Lpr lFf">
    <q-header elevated>
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="toggleLeftDrawer"
        />

        <q-toolbar-title v-if="$q.screen.gt.xs" shrink class="row items-center no-wrap">
          <span class="q-ml-xs" style="font-size: 15px">TAGUM CITY YOUTH INFORMATION SYSTEM</span>
        </q-toolbar-title>

        <q-space />

        <div class="q-gutter-sm row items-center no-wrap">
          <q-btn
            flat
            class="logout-button"
            @click="logout"
          >
            Log Out
          </q-btn>
        </div>
      </q-toolbar>
    </q-header>

    <q-drawer
  v-model="leftDrawerOpen"
  show-if-above
  bordered
  :width="280"
  style="background-color: #14662b;">  
  
  <div class="q-pa-md">
          <q-img
  src="panda.jpg"
  spinner-color="white"
  class="q-img-container my-custom-image"
/>

  <div class="text-subtitle1 text-center" style="color: white">Boss Ken</div>
    <div class="text-h6 q-mt-sm text-center" style="color: white">Admin</div>
</div>



      <q-scroll-area class="fit">
        <q-list padding class="text-grey-8">
          <q-item
            clickable
            v-ripple
            @click="handleItemClick"
            :class="{ 'active-item': selectedSection === 'dashboard' }"
            
          >
            <q-item-section avatar>
              <q-avatar
                rounded
                :style="{
                  'background-color':
                    selectedSection === 'dashboard' ? '#0e7c2b' : '#5f6368',
                }"
                text-color="white"
                icon="dashboard"
              >
              </q-avatar>
            </q-item-section>


            
            

            <q-item-section class="responsive-text" >
              <q-item-label style="color: white;"> <b>Home</b> </q-item-label>
            </q-item-section>
          </q-item>


          
          <q-expansion-item group="somegroup" v-model="management">
            <template v-slot:header>
              <q-item-section avatar>
                <q-avatar
                  rounded
                  text-color="white"
                  icon="list"
                  size="40px"
                  :style="{
                    'background-color':
                      management === true ? '#0e7c2b' : '#5f6368',
                  }"
                ></q-avatar>
              </q-item-section>

              <q-item-section class="responsive-text">
                <q-item-label style="color: white;"> <b>Admin Menu</b> </q-item-label>
              </q-item-section>
            </template>

            <q-item
              clickable
              v-ripple
              @click="toggleSection('add_user')"
              :class="{ 'active-item': selectedSection === 'add_user' }"
            >
              <q-item-section class="q-ml-sm">
                <q-item-label style="color: white;" >
                  <q-icon
                    :style="{
                      color:
                        selectedSection === 'add_user'
                          ? '#006400'
                          : 'inherit',
                    }"
                    name="groups"
                    class="q-ml-md q-mr-md"
                  />
                  Add User Account</q-item-label
                >
              </q-item-section>
            </q-item>

            <q-item
  clickable
  v-ripple
  @click="toggleSection('enumertors_record')"
  :class="{ 'active-item': selectedSection === 'enumertors_record' }"
>
  <q-item-section class="q-ml-sm">
    <q-item-label style="color: white;">
      <q-icon
        :style="{
          color:
            selectedSection === 'enumertors_record'
              ? '#006400'
              : 'inherit',
        }"
        name="groups"
        class="q-ml-md q-mr-md"
      />
      Enumerators Record
    </q-item-label>
  </q-item-section>
</q-item>

          </q-expansion-item>

          
          

          <q-expansion-item group="somegroup" v-model="youthRecord">
  <template v-slot:header>
    <q-item-section avatar>
      <q-avatar
        rounded
        text-color="white"
        icon="find_in_page"
        size="40px"
        :style="{
          'background-color': youthRecord === true ? '#0e7c2b' : '#5f6368',
        }"
      ></q-avatar>
    </q-item-section>
    <q-item-section class="responsive-text">
      <q-item-label style="color: white;"> <b>Youth Record</b> </q-item-label>
    </q-item-section>
  </template>

  <q-item
  clickable
  v-ripple
  @click="toggleSection('search_record')"
  :class="{ 'active-item': selectedSection === 'search_record' }"
>

    <q-item-section class="q-ml-sm">
      <q-item-label style="color: white;">
        <q-icon
          :style="{
            color: selectedSection === 'search_record' ? '#0e7c2b' : 'inherit',
          }"
          name="search"
          class="q-ml-md q-mr-md"
        />
        Search Record
      </q-item-label>
    </q-item-section>
  </q-item>

  <q-item
    clickable
    v-ripple
    @click="toggleSection('add_record')"
    :class="{ 'active-item': selectedSection === 'add_record' }"
  >
    <q-item-section class="q-ml-sm">
      <q-item-label style="color: white;">
        <q-icon
          :style="{
            color: selectedSection === 'add_record' ? '#0e7c2b' : 'inherit',
          }"
          name="add_circle"
          class="q-ml-md q-mr-md"
        />
        Add Record
      </q-item-label>
    </q-item-section>
  </q-item>
</q-expansion-item>





<q-expansion-item group="somegroup" v-model="eventsMenu">
  <template v-slot:header>
    <q-item-section avatar>
      <q-avatar
        rounded
        text-color="white"
        icon="event"
        size="40px"
        :style="{
          'background-color': eventsMenu === true ? '#0e7c2b' : '#5f6368',
        }"
      ></q-avatar>
    </q-item-section>
    <q-item-section class="responsive-text">
      <q-item-label style="color: white;"> <b>Events Menu</b> </q-item-label>
    </q-item-section>
  </template>

  <q-item
    clickable
    v-ripple
    @click="toggleSection('create_events')"
    :class="{ 'active-item': selectedSection === 'create_events' }"
  >
    <q-item-section class="q-ml-sm">
      <q-item-label style="color: white;">
        <q-icon
          :style="{
            color: selectedSection === 'create_events' ? '#0e7c2b' : 'inherit',
          }"
          name="event"
          class="q-ml-md q-mr-md"
        />
        Create Events
      </q-item-label>
    </q-item-section>
  </q-item>

  <q-item
    clickable
    v-ripple
    @click="toggleSection('attendance')"
    :class="{ 'active-item': selectedSection === 'attendance' }"
  >
    <q-item-section class="q-ml-sm">
      <q-item-label style="color: white;">
        <q-icon
          :style="{
            color: selectedSection === 'attendance' ? '#0e7c2b' : 'inherit',
          }"
          name="check_circle"
          class="q-ml-md q-mr-md"
        />
        Attendance
      </q-item-label>
    </q-item-section>
  </q-item>
</q-expansion-item>
  </q-list>
      </q-scroll-area>
    </q-drawer>


   <!-- Main content area -->
   <q-page-container v-if="DashboardView">
      <DashboardView />
    </q-page-container>

    <q-page-container v-if="showAddUser">
      <Add_user />
    </q-page-container>

    <q-page-container v-if="showSearchRecord">
      <Search_record />
    </q-page-container>

    <q-page-container v-if="showCreateEvents">
      <Create_events />
    </q-page-container>

    <q-page-container v-if="showAttendance">
      <Attendance />
    </q-page-container>

    <q-page-container v-if="showEnumeratorsRecord">
      <Enumerators_record />
    </q-page-container>
  </q-layout>
</template>

<script>
import { defineComponent, ref } from "vue";
// import EssentialLink from "components/EssentialLink.vue";
import Add_user from "components/Add_user.vue";
import DashboardView from "src/components/DashboardView.vue";
import Search_record from "src/components/Search_record.vue";
import Create_events from "src/components/Create_events.vue";
import Attendance from "src/components/Attendance.vue";
import Enumerators_record from "src/components/Enumerators_record.vue";

const linksList = [
  {
    title: "Admin",
    // caption: 'quasar.dev',
    caption: "",
    icon: "home",
    link: "https://quasar.dev",
  },
  {
    title: "Github",
    caption: "github.com/quasarframework",
    icon: "code",
    link: "https://github.com/quasarframework",
  },
];

export default defineComponent({
  name: "MainLayout",

  components: {
    // EssentialLink,
    Add_user,
    DashboardView,
    Search_record,
    Create_events,
    Attendance,
    Enumerators_record,
  },

  setup() {
    const leftDrawerOpen = ref(false);

    return {
      essentialLinks: linksList,
      leftDrawerOpen,
      toggleLeftDrawer() {
        leftDrawerOpen.value = !leftDrawerOpen.value;
      },
    };
  },
  data() {
    return {
      selectedSection: "dashboard",
      DashboardView: true,
      showAddUser: false,
      showSearchRecord: false,
      showCreateEvents: false,
      showAttendance: false,
      showEnumeratorsRecord: false,
      management: false,
      youthRecord: false,
      eventsMenu: false,
    };
  },
  methods: {
  handleItemClick() {
    this.toggleSection("dashboard");
  },
  toggleSubMenu() {
    this.submenuOpen = !this.submenuOpen;
  },
  closeSubMenu() {
    this.submenuOpen = false;
  },
  toggleSection(section) {
  this.showAddUser = section === 'add_user';
  this.showSearchRecord = section === 'search_record';
  this.DashboardView = section === 'dashboard';
  this.showCreateEvents = section === 'create_events';
  this.showAttendance = section === 'attendance';
  this.showEnumeratorsRecord = section === 'enumerators_record';

  // Ensure correct state for other expansion items
  this.management = section === 'add_user' || section === 'enumerators_record';
  this.youthRecord = section === 'search_record' || section === 'add_record';
  this.eventsMenu = section === 'create_events' || section === 'attendance';

  if (this.selectedSection === section) {
    // Toggle section visibility on subsequent clicks
    this.selectedSection = null;
  } else {
    this.selectedSection = section;
  }
},
},
});
</script>



<style scoped>
.custom-drawer-bg {
  background-color: #317543; /* Use your preferred shade of green */
}

.GNL__toolbar {
  height: 64px;
}

.GNL__toolbar-input {
  width: 55%;
}

.GNL__drawer-item {
  line-height: 24px;
  border-radius: 0 24px 24px 0;
  margin-right: 12px;
}

.GNL__drawer-item .q-item__section--avatar .q-icon {
  color: #5f6368;
}

.GNL__drawer-item .q-item__label {
  color: #3c4043;
  letter-spacing: 0.01785714em;
  font-size: 0.875rem;
  font-weight: 500;
  line-height: 1.25rem;
}

.GNL__drawer-footer-link {
  color: inherit;
  text-decoration: none;
  font-weight: 500;
  font-size: 0.75rem;
}

.GNL__drawer-footer-link:hover {
  color: #000;
}

.q-img-container {
  display: flex;
  justify-content: center; 
  align-items: center; 
  height: 100px; 
  max-width: 100px; 
  border-radius: 100%; 
  margin: 0 auto; 
}

.my-custom-image {
  width: 100%; 
  height: auto; 
  border-radius: 100%; 
}













</style>
