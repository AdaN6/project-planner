<template>
  <div class="home">
    <FilterNav @filterChange="current = $event" :current="current"/>
    <div v-if="projects.length">
      <div v-for="project in filteredProjects" :key="project.id">
        <SingleProject :project="project" @delete="handleDelete" @complete="handleComplete"/>
      </div>
    </div>
  </div>
</template>

<script>

import SingleProject from '../components/SinglePorject.vue'
import FilterNav from '../components/FilterNav.vue'

export default {
  name: 'HomeView',
  components: { SingleProject, FilterNav},
  data() {
    return {
      projects: [],
      current: 'all'
    }
  },
  // mounted life cycle hook
  mounted() {
    fetch('http://localhost:3000/projects')
    .then(res => res.json())
    .then(data => this.projects = data)
    .catch(err => console.log(err.message))
  },
  methods: {
    handleDelete(projID) {
      this.projects = this.projects.filter((project) => {
        return project.id !== projID
      })
    },
    handleComplete(projID){
      let p = this.projects.find((proj) => {
        return proj.id === projID
      })
      p.complete = !p.complete
    }
  },
  computed: {
        filteredProjects() {
            if(this.current === 'done' ) {
              return this.projects.filter(project => project.complete)
            }
            if(this.current === 'toDo' ) {
              return this.projects.filter(project => !project.complete)
            }
            return this.projects
        }
    }
}
</script>
