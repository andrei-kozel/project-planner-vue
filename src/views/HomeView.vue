<template>
  <div v-for="project in projects" :key="project.id" @add="handleAdd">
    <ProjectItem :project="project" />
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
    handleAdd(project: Project) {
      console.log(project);
    },
  },
});
</script>
x
<style scoped></style>
