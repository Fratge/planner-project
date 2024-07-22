<template>
  <FilterNav :current="current" @filterChange="current = $event" />
  <div v-if="this.projects.length">
    <div v-for="project in filteredProjects" :key="project.id">
      <SingleProjectVue :data="project" @delete="handleDelete" @complete="handleComplete"/>
    </div>
  </div>
</template>

<script>
import SingleProjectVue from '@/components/SingleProject.vue';
import FilterNav from '@/components/FilterNav.vue';

export default {
  name: '',
  components: {
    SingleProjectVue,
    FilterNav,
  },
  data(){
    return {
      projects: [],
      current: 'viewAll',
    }
  },
  mounted(){
    fetch('http://localhost:3000/projects')
    .then(response => response.json())
    .then(data => {
      this.projects = data
    })
    .catch(err => console.log(err.message));
  },
  methods: {
    handleDelete(id){
      this.projects = this.projects.filter((project) => project.id !== id);
    },

    handleComplete(id){
      let p = this.projects.find((project) => {
        return project.id === id;
      });
      p.complete = !p.complete;
    },
  },
  computed: {
    filteredProjects() {
      if (this.current === 'completed') {
        return this.projects.filter(project => project.complete)
      }
      if (this.current === 'onGoing') {
        return this.projects.filter(project => !project.complete)
      }
      return this.projects
    }
  }
}
</script>
