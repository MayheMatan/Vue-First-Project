<template>
  <base-card>
    <base-button
      @click="activateComponent('stored-resources')"
      :mode="storedResMode"
      >Stored Resources</base-button
    >
    <base-button @click="activateComponent('add-resource')" :mode="addResMode"
      >Add Resource</base-button
    >
  </base-card>
  <keep-alive>
    <component :is="activeTab"></component>
  </keep-alive>
</template>

<script>
import StoredResources from "./StoredResources";
import AddResource from "./AddResources";

export default {
  components: {
    StoredResources,
    AddResource,
  },
  data() {
    return {
      activeTab: "stored-resources",
      storedResources: [
        {
          id: "Google",
          title: "Google",
          description: "The most coolest site for searching",
          url: "https://www.google.com",
        },
        {
          id: "Vue",
          title: "Vue",
          description: "The most reactive tool for building UI interface",
          url: "https://vuejs.org/",
        },
      ],
    };
  },
  computed: {
    storedResMode() {
      return this.activeTab === "stored-resources" ? null : "flat";
    },
    addResMode() {
      return this.activeTab === "add-resource" ? null : "flat";
    },
  },
  provide() {
    return {
      resources: this.storedResources,
      addResource: this.addResource,
      deleteResource: this.deleteResource,
    };
  },
  methods: {
    activateComponent(component) {
      this.activeTab = component;
    },
    addResource(title, description, url) {
      const newResource = {
        id: new Date().toISOString(),
        title,
        description,
        url,
      };
      this.storedResources.unshift(newResource);
      this.activeTab = "stored-resources";
    },
    deleteResource(resourceId) {
      const indexToRemove = this.storedResources.findIndex(
        (resource) => resource.id === resourceId
      );
      this.storedResources.splice(indexToRemove, 1);
    },
  },
};
</script>
