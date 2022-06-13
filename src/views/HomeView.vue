<template>
  <FilterNavigation @update="current = $event" :current="current" />
  <div v-for="project in filteredProjects" :key="project.id">
    <ProjectItem :project="project" @delete="handleDelete" @done="handleDone" />
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import ProjectItem from "@/components/ProjectItem.vue";
import FilterNavigation from "@/components/FilterNavigation.vue";

interface Project {
  id: number;
  title: string;
  details: string;
  completed: boolean;
}

export default defineComponent({
  components: {
    ProjectItem,
    FilterNavigation,
  },
  data() {
    return {
      projects: [] as Project[],
      current: "all",
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
    updateFilter() {
      this.projects = this.projects.filter((project) => {
        return project.completed === false;
      });
    },
  },
  computed: {
    filteredProjects(): Project[] {
      if (this.current === "ongoing") {
        return this.projects.filter((project: Project) => !project.completed);
      } else if (this.current === "completed") {
        return this.projects.filter((project: Project) => project.completed);
      }
      return this.projects;
    },
  },
});
</script>
<style scoped></style>
