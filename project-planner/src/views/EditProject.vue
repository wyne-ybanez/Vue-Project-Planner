<template>
  <form @submit.prevent="handleSubmit">
    <label>Title</label>
    <input type="text" v-model="title" required>
    <label>Details</label>
    <textarea v-model="details" required></textarea>
    <button>Update Project</button>
  </form>
</template>

<script>
export default {
  props: ['id'], // SingleProject.vue -> project.id
  data() {
    return {
      uri: 'http://localhost:3000/projects/' + this.id,
      title: '',
      details: '',
    }
  },
  // once mounted on the DOM, get json data and attach to data above
  mounted() {
    fetch(this.uri)
      .then(res => res.json())
      .then(data => {
        this.title = data.title
        this.details = data.details
      }).catch(err => console.log(err))
  },
  methods: {
    /*
    update the project and save the new data to db.json
    - use the fetch api to send a PATCH request to update -> dependent on uri & id
    - stringify the updates for the server, needs to be stringified as this is an object
    - redirect to homepage when finished
    */
    handleSubmit() {
      fetch(this.uri, {
        method: 'PATCH',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ title: this.title, details: this.details })
      }).then(() => {
        this.$router.push('/')
      }).catch(err => console.log(err))
    }
  }
}
</script>

<style>

</style>