<template>
  <div>
    <base-card>
      <base-button
        :mode="storedResButtonMode"
        @click.native="setSelectedTab('stored-resources')"
      >
        Stored Resources
      </base-button>
      <base-button
        :mode="addResButtonMode"
        @click.native="setSelectedTab('add-resource')"
      >
        Add Resource
      </base-button>
    </base-card>
    <keep-alive>
      <component :is="selectedTab"></component>
    </keep-alive>
  </div>
</template>

<script>
import StoredResources from './StoredResources.vue'
import AddResource from './AddResource.vue'

export default {
  components: { AddResource, StoredResources },
  data() {
    return {
      selectedTab: 'stored-resources',
      storedResources: [
        {
          id: 'official-guide',
          title: 'Official Guide',
          description: 'The official Vue.js documentation',
          link: 'https://vuejs.org',
        },
        {
          id: 'google',
          title: 'Google',
          description: 'Learn to google...',
          link: 'https://google.com',
        },
      ],
    }
  },
  provide() {
    return {
      resources: this.storedResources,
      addResource: this.addResource,
      deleteResource: this.removeResource,
    }
  },
  computed: {
    storedResButtonMode() {
      return this.selectedTab === 'stored-resources' ? null : 'flat'
    },
    addResButtonMode() {
      return this.selectedTab === 'add-resource' ? null : 'flat'
    },
  },
  methods: {
    setSelectedTab(tab) {
      this.selectedTab = tab
    },
    addResource(titleInput, descriptionInput, urlInput) {
      const newResource = {
        id: new Date().toISOString(),
        title: titleInput,
        description: descriptionInput,
        link: urlInput,
      }
      this.storedResources.unshift(newResource)
      this.selectedTab = 'stored-resources'
    },
    removeResource(resId) {
      const resIndex = this.storedResources.findIndex((res) => res.id === resId)
      this.storedResources.splice(resIndex, 1)
    },
  },
}
</script>
