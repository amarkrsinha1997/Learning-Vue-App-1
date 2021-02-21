<template>
  <base-card>
    <base-button
      @click="setSelectedTab('stored-resources')"
      :mode="storedResButtonMode"
    >
      Stored Resources
    </base-button>
    <base-button
      @click="setSelectedTab('add-resource')"
      :mode="addResButtonMode"
    >
      Add Resource
    </base-button>
  </base-card>
  <keep-alive>
    <component :is="selectedTab" />
  </keep-alive>
</template>
<script>
import AddResource from './AddResource.vue';
import StoredResources from './StoredResources.vue';
const componentNames = {
  STORED_RESOURCES: 'stored-resources',
  ADD_RESOURCES: 'add-resource',
};
export default {
  components: {
    [componentNames.ADD_RESOURCES]: AddResource,
    [componentNames.STORED_RESOURCES]: StoredResources,
  },
  data() {
    return {
      selectedTab: componentNames.STORED_RESOURCES,
      storedResources: [
        {
          id: 'official-guide',
          title: 'Oficial Guide',
          description: 'The official Vue.js documentation.',
          link: 'https://vuejs.org',
        },
        {
          id: 'google-search',
          title: 'Searching Google',
          description: 'Learn to search google',
          link: 'https://google.com',
        },
      ],
    };
  },
  computed: {
    storedResButtonMode() {
      return this.selectedTab === componentNames.STORED_RESOURCES ? '' : 'flat';
    },
    addResButtonMode() {
      return this.selectedTab === componentNames.ADD_RESOURCES ? '' : 'flat';
    },
  },
  provide() {
    return {
      resources: this.storedResources,
      addResource: this.addResources,
      removeResources: this.removeResources,
    };
  },
  methods: {
    setSelectedTab(tab) {
      this.selectedTab = tab;
    },
    addResources(resource) {
      this.storedResources.unshift({
        ...resource,
        id: resource.title.toLowerCase().split(' ').join('-'),
      });
      this.selectedTab = componentNames.STORED_RESOURCES;
    },
    removeResources(resourceId) {
      const resourceIndex =  this.storedResources.findIndex(
        (resource) => resource.id === resourceId
      );
      this.storedResources.splice(resourceIndex, 1)
    },
  },
};
</script>
<style scoped>
</style>