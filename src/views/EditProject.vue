<template>
  <form class="form" @submit.prevent="handleSubmit">
    <div class="input-group">
      <label for="title">Title</label>
      <input name="title" placeholder="Project title" v-model="title" />
    </div>
    <div class="input-group">
      <label for="details">Details</label>
      <textarea
        name="details"
        placeholder="Project details"
        v-model="details"
      />
    </div>
    <button class="btn" type="submit">Save</button>
  </form>
</template>

<script lang="ts">
import { defineComponent } from "vue";

interface Project {
  title: string;
  details: string;
  completed: boolean;
}

export default defineComponent({
  props: ["id"],
  data() {
    return {
      title: "",
      details: "",
      url: "http://localhost:3000/projects/" + this.id,
    };
  },
  methods: {
    handleSubmit() {
      let project: Project = {
        title: this.title,
        details: this.details,
        completed: false,
      };

      fetch(this.url, {
        method: "PATCH",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(project),
      })
        .then(() => {
          this.$router.push("/");
        })
        .catch((err) => console.log(err));
    },
  },
  mounted() {
    fetch(this.url, {
      method: "GET",
      headers: {
        "Content-Type": "text/plain",
      },
    })
      .then((res) => res.json())
      .then((data) => {
        this.title = data.title;
        this.details = data.details;
      })
      .catch((err) => console.log(err));
  },
});
</script>

<style scoped>
.form {
  @apply flex flex-col w-full m-2;
  max-width: 500px;
}
.input-group {
  @apply mb-4 flex flex-col w-full text-left;
}

.input-group label {
  @apply text-gray-600 text-sm font-bold;
}

.input-group input {
  @apply border border-gray-300 rounded-md p-2;
}

.input-group textarea {
  @apply border border-gray-300 rounded-md p-2;
}

.btn {
  @apply bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded-md w-36 m-auto;
}
</style>
