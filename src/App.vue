<template>
  <v-app>
    <v-app-bar
      app
      dark
      clipped-left
      src="https://images.unsplash.com/photo-1618004912476-29818d81ae2e?ixlib=rb-1.2.1&raw_url=true&q=80&fm=jpg&crop=entropy&cs=tinysrgb&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1528"
    >
      <div>
        <v-img
          alt="workers list app logo"
          size="80"
          contain
          src="./assets/logo-nav.png"
          transition="scale-transition"
          width="50"
        />
      </div>

      <v-row>
        <span class="ml-6 text-md-h5 text-sm-subtitle-1 text-xs-caption" color="white"><b>Employees</b></span>
      </v-row>
      <v-spacer></v-spacer>
      <div>
      <v-row>
        <v-icon class="mr-4">mdi-message</v-icon>
        <v-icon class="mr-4">mdi-bell</v-icon>
        <v-avatar size="50" class="blue mr-4">
						<v-img
						src="./assets/dashboard-user.jpg"
						alt="user photo"
						contain
						></v-img>
				</v-avatar>
        <v-row class="align-center">
        <v-col>
          <p class="white--text text-subtitle-2 mb-0 pb-0">Beff Jezos</p>
          <p class="white--text text-caption mb-0 pb-0">Head of HR</p>
        </v-col>
        </v-row>
        <v-icon class="mr-16 ml-2">mdi-chevron-down</v-icon>
      </v-row>
      </div>
    </v-app-bar>
    
    <v-navigation-drawer
      absolute
      dark
      src="https://images.unsplash.com/photo-1620641788421-7a1c342ea42e?crop=entropy&cs=tinysrgb&fm=jpg&ixlib=rb-1.2.1&q=80&raw_url=true&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1548"
      expand-on-hover
      permanent
      class="mt-14"
    >
      <v-list>
        <v-list-item
          v-for="([icon, text], i) in sidebarItems"
          :key="i"
          link
        >
          <v-list-item-icon>
            <v-icon>{{ icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ text }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>


    <v-main>
      <!-- <HelloWorld/> -->
      <workerList/>
    </v-main>
  </v-app>
</template>

<script>
// import HelloWorld from './components/HelloWorld';
import workerList from './components/workerList';

export default {
  name: 'App',

  components: {
    // HelloWorld,
    workerList
  },

  data: () => ({
    sidebarItems: [
        ['mdi-view-dashboard-outline', 'Dashboard'],
        ['mdi-account-supervisor-circle', 'Employees'],
        ['mdi-calendar-check', 'Tasks'],
        ['mdi-tune-vertical', 'Settings'],
        ['mdi-help', 'Help'],
      ],
  }),
};
</script>

<style>
	.v-main__wrap {
    background: #BBDEFB;
    padding: 0 6rem;
	};

  div {
		border: 1px solid red;
	};
</style>