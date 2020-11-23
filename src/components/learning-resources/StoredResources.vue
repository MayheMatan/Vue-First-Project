<template>
  <ul>
    <LearningResources
      v-for="resource in resources"
      :key="resource.id"
      :title="resource.title"
      :description="resource.description"
      :url="resource.url"
      :id="resource.id"
    />
  </ul>
</template>

<script>
import LearningResources from "./LearningResources";

export default {
  components: {
    LearningResources,
  },
  inject: ["resources"],
};
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
  margin: auto;
  max-width: 40rem;
}
</style>
