<template>
  <base-card>
    <base-button @click="setSelectedTab('stored-resources')" :mode="storedResButtonMode">Stored Resources</base-button>
    <base-button @click="setSelectedTab('add-resources')" :mode="addResButtonMode">Add Resources</base-button>
  </base-card>
  <keep-alive>
    <component :is="selectedTab"></component>
  </keep-alive>  
</template>

<script>

import StoredResources from './StoredResources';
import AddResources from './AddResource';

export default {
  components:{
    'stored-resources': StoredResources,
    'add-resources': AddResources,
  },
  data() {
    return{
      selectedTab : 'stored-resources',
      storedResources: [
        {
          id: 'official-guide',
          title: 'Official Guide', 
          description: 'The Official VueJs Dcumentation',
          link:'https://vuejs.org/'
        },
        {
          id: 'google',
          title: 'Google', 
          description: 'Learn to Google...',
          link:'https://google.org/'
        }
      ]
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
      return this.selectedTab === 'stored-resources' ? null : 'flat';
    },
    addResButtonMode() {
      return this.selectedTab === 'add-resources' ? null : 'flat';
    }
  },
  methods: {
    setSelectedTab(tab){
      this.selectedTab = tab
    },
    addResource(title, description, url){
      const newResource = {
        id: new Date().toISOString,
        title,
        description,
        link: url
      }
      this.storedResources.unshift(newResource);
      this.selectedTab = 'stored-resources';
    },
    removeResource(resId){
      const resIndex = this.storedResources.findIndex(res => res.id === resId);
      this.storedResources.splice(resIndex,1);
    }
  }
}
</script>




