<template>
  <ul>
    <learning-resource
      v-for="resource in resources"
      :key="resource.id" 
      :res='resource'
    ></learning-resource>
  </ul>
</template>


<script>

import LearningResource from './LearningResource';
export default {
  inject:['resources'],
  components:{
    'learning-resource' : LearningResource
  },
}
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