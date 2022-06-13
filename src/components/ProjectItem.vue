<template>
  <div class="project container" :class="{ pdone: project.completed }">
    <div class="actions">
      <p class="title" @click="toggleShowDetails">{{ project.title }}</p>
      <div class="icons">
        <span class="material-icons icon" @click="editProject"> edit </span>
        <span class="material-icons icon" @click="deleteProject"> delete </span>
        <span
          class="material-icons icon"
          @click="doneProject"
          :class="{ done: project.completed }"
        >
          done
        </span>
      </div>
    </div>
    <p v-if="showDetails" class="description">{{ project.details }}</p>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  props: ["project"],
  data() {
    return {
      showDetails: false,
      url: "http://localhost:3000/projects/" + this.project.id,
    };
  },
  methods: {
    toggleShowDetails() {
      this.showDetails = !this.showDetails;
    },
    editProject() {
      console.log("edit");
    },
    deleteProject() {
      fetch(this.url, {
        method: "DELETE",
      }).then(() => {
        this.$emit("delete", this.project.id);
      });
    },

    doneProject() {
      fetch(this.url, {
        method: "PATCH",
        headers: {
          "Content-Type": "application/json",
        },
        body: JSON.stringify({ completed: !this.project.completed }),
      })
        .then(() => {
          this.$emit("done", this.project.id);
        })
        .catch((err) => console.log(err));
    },
  },
});
</script>

<style scoped>
.project.container {
  @apply border border-gray-300 rounded-md py-4 px-2 m-2 flex flex-col items-start border-l-4 border-l-red-400;
  width: 600px;
}

.pdone {
  @apply border-l-4 !border-l-green-400;
}

.project {
  @apply bg-white;
}

.actions {
  @apply w-full flex justify-between;
}
.icon {
  @apply text-gray-400 hover:text-gray-600 mx-1 cursor-pointer;
}

.title {
  @apply text-gray-600 text-xl font-bold  cursor-pointer hover:text-gray-800;
}

.description {
  @apply text-gray-500 mt-2 text-left;
}

.done {
  @apply text-green-400;
}
</style>
