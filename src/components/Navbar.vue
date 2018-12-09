<template>
  <nav>
    <v-toolbar flat app>
      <v-toolbar-side-icon class="grey--text" @click="drawer = !drawer"></v-toolbar-side-icon>
      <v-toolbar-title class="text-uppercase grey--text">
        <span class="font-weight-light">Todo</span>
        <span>Dashboard</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>

      <!-- Dropdown Menu -->
      <v-menu offset-y>
        <v-btn flat slot="activator" color="grey">
          <v-icon>expand_more</v-icon>
          <span>Menu</span>
        </v-btn>
        <v-list>
          <v-list-tile v-for="l in links" :key="l.text" router :to="l.route">
            <v-list-tile-title>{{l.text}}</v-list-tile-title>
          </v-list-tile>
        </v-list>
      </v-menu>

      <v-btn flat color="grey">
        <span>Sign Out</span>
        <v-icon right>exit_to_app</v-icon>
      </v-btn>
    </v-toolbar>

    <v-navigation-drawer v-model="drawer" app class="primary">
      <v-layout column align-center class="lighten-4 grey">
        <v-flex class="mt-5">
          <v-avatar size="100">
            <img
              src="data:image/png;base64,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"
              alt="Avatar"
            >
          </v-avatar>
          <p class="black--text subheading mt-1 text-xs-center">Ayanrocks</p>
        </v-flex>
        <v-flex class="mt-4 mb-3">
          <Popup @addProject="addProject"/>
        </v-flex>
      </v-layout>
      <v-list>
        <v-list-tile v-for="link in links" :key="link.text" router :to="link.route">
          <v-list-tile-action>
            <v-icon class="white--text">{{link.icon}}</v-icon>
          </v-list-tile-action>
          <v-list-tile-content>
            <v-list-tile-title class="white--text">{{link.text}}</v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
      </v-list>
    </v-navigation-drawer>
  </nav>
</template>

<script>
import Popup from "./Popup";

export default {
  components: {
    Popup
  },
  data() {
    return {
      drawer: false,
      links: [
        { icon: "dashboard", text: "Dashboard", route: "/" },
        { icon: "folder", text: "My Projects", route: "/projects" },
        { icon: "person", text: "Team", route: "/team" }
      ]
    };
  },
  methods: {
    addProject(data) {
      console.log(data);
    }
  }
};
</script>
