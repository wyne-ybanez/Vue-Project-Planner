<template>
  <div class="home">
    <FilterNav :current="current" @filterChange="current = $event" />
    <div v-if="projects.length">
      <div v-for="project in filteredProjects" :key="project.id">
      <SingleProject :project="project" @delete="handleDelete" @complete="handleComplete" />
      </div>
    </div>
  </div>
</template>

<script>
import SingleProject from '../components/SingleProject.vue'
import FilterNav from '../components/FilterNav.vue'

export default {
  name: 'Home',
  components: { SingleProject, FilterNav },
  data() {
    return {
      projects: [],
      current: 'all',
    };
  },
  /*
   - fetch data when view is mounted on DOM
   - update projects array with data we receive
  */
  mounted() {
    fetch('http://localhost:3000/projects')
      .then(res => res.json())
      .then(data => this.projects = data)
      .catch(err => console.log(err))
  },
  methods: {
     /*
      Handles Delete (SingleProject.vue -> id)
      - once emit is received, it filters for projects without the emitted project ID
      - we do this because when we delete data, it must also be done at the local level
     */
    handleDelete(id) {
      this.projects = this.projects.filter(project => {
        return project.id !== id
      })
    },
    /*
      Handles Complete (SingleProject.vue -> id)
      - update, find first then set variable
      - if found (true), set it to 'p' variable
    */
    handleComplete(id) {
      let p = this.projects.find(project => {
        return project.id === id
      })
      p.complete = !p.complete
    }
  },
  computed: {
    filteredProjects() {
      if (this.current === 'completed') {
        return this.projects.filter(project => project.complete)
      }
      if (this.current === 'ongoing') {
        return this.projects.filter(project => !project.complete)
      }
      return this.projects
    }
  },
}
</script>
