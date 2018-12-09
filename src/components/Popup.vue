<template>
  <v-dialog max-width="600px">
    <v-btn slot="activator" flat class="success">Add New Project</v-btn>
    <v-card>
      <v-card-title>
        <h2>Add a New Project</h2>
      </v-card-title>
      <v-card-actions class="text-xs-center">
        <v-layout row wrap align-center>
          <v-flex xs6 md12>
            <v-text-field v-model="name" label="Name" required flat></v-text-field>
          </v-flex>
          <v-flex xs6 md12>
            <v-text-field v-model="project" label="Project" required></v-text-field>
          </v-flex>
          <v-flex xs6 md12>
            <v-text-field v-model="due" label="Due Date" required></v-text-field>
          </v-flex>
          <v-flex xs6 md12>
            <v-text-field v-model="status" label="Status" required></v-text-field>
          </v-flex>
          <v-flex xs6 md12 class="my-3">
            <v-btn class="success" @click="addProject">Add Project
              <v-icon right>send</v-icon>
            </v-btn>
          </v-flex>
        </v-layout>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>


<script>
export default {
  data() {
    return {
      name: "Ayanrocks",
      project: "",
      due: "",
      status: ""
    };
  },
  methods: {
    addProject() {
      var data = {
        name: this.name,
        project: this.project,
        due: this.due,
        status: this.status.toLowerCase()
      };

      this.$emit("addProject", data);
    }
  }
};
</script>
