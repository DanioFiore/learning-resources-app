<template>
  <base-card>
    <base-button
      @click="setSelectedTab('stored-resources')"
      :mode="storedResButtonMode"
      >Stored Resources</base-button
    >
    <base-button
      @click="setSelectedTab('add-resource')"
      :mode="addResButtonMode"
      >Add Resource</base-button
    >
  </base-card>
  <keep-alive>
    <component :is="selectedTab"></component>
  </keep-alive>
</template>

<script>
import StoredResources from './StoredResources.vue';
import AddResource from './AddResource.vue';

export default {
  computed: {
    storedResButtonMode() {
      return this.selectedTab === 'stored-resources' ? null : 'flat';
    },
    addResButtonMode() {
      return this.selectedTab === 'add-resource' ? null : 'flat';
    },
  },
  components: {
    StoredResources,
    AddResource,
  },
  data() {
    return {
      selectedTab: 'stored-resources',
      storedResources: [
        {
          id: 1,
          title: 'Vue Official Guide',
          description: 'The official guide of vue.js',
          link: 'https://vuejs.org',
        },
        {
          id: 2,
          title: 'Google',
          description: 'Learn to google',
          link: 'https://google.com',
        },
      ],
    };
  },

  provide() {
    return {
      resources: this.storedResources,
      addResource: this.addResource,
      deleteResource: this.deleteResource,
    };
  },

  methods: {
    setSelectedTab(tab) {
      this.selectedTab = tab;
    },

    addResource(id, title, description, link) {
      this.storedResources.unshift({
        id: id,
        title: title,
        description: description,
        link: link,
      });
      this.selectedTab = 'stored-resources';
    },

    deleteResource() {
         const resIndex = this.storedResources.findIndex(res => res.id)
         this.storedResources.splice(resIndex, 1);

    }
  },
};
</script>
