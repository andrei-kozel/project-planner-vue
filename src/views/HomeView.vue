<template>
  <div v-for="project in projects" :key="project.id">
    <ProjectItem :project="project" @delete="handleDelete" @done="handleDone" />
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import ProjectItem from "@/components/ProjectItem.vue";

interface Project {
  id: number;
  title: string;
  details: string;
  completed: boolean;
}

export default defineComponent({
  components: {
    ProjectItem,
  },
  data() {
    return {
      projects: [] as Project[],
    };
  },
  mounted() {
    fetch("http://localhost:3000/projects", {
      method: "Get",
      headers: {
        "Content-Type": "text/plain",
      },
    })
      .then((res) => res.json())
      .then((data) => {
        this.projects = data;
      })
      .catch((err) => console.log(err));
  },
  methods: {
    handleDelete(id: number) {
      this.projects = this.projects.filter((project) => project.id !== id);
    },
    handleDone(id: number) {
      this.projects = this.projects.map((project) => {
        if (project.id === id) {
          project.completed = !project.completed;
        }
        return project;
      });
    },
  },
});
</script>
x
<style scoped></style>
