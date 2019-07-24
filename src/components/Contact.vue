<template>
  <div>
    <div class="row">
      <div class="col-sm-6 mb-3 mb-md-0 col-centered">
        <div class="card">
          <div v-if="$route.params.id > 0" class="card-header">
             Edit contact name
          </div>
          <div v-else class="card-header">
             Add new contact
          </div>
          <div class="card-body">
            <form @submit="contactFormSubmit">
              <p>
                <label for="name">Name</label>
                <input
                  v-model="name"
                  type="text"
                  name="name"
                >
              </p>
              <p>
                <input
                  type="submit"
                  class="btn btn-success"
                  value="Save"
                >
              </p>
            </form>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Contact',
  data () {
    return {
      id: null,
      name: null
    }
  },
  methods: {
    contactFormSubmit (e) {
      e.preventDefault()
      if (!this.id) {
        this.axios.post('/contact', {name: this.name})
          .then((response) => {
            this.$router.push('/')
          })
      } else {
        this.axios.put('/contact/' + this.id, {name: this.name})
          .then((response) => {
            this.$router.push('/')
          })
      }
    }
  },
  mounted () {
    if (this.$route.params.id) {
      this.axios.get('/contact/' + this.$route.params.id)
        .then((response) => {
          this.id = this.$route.params.id
          this.name = response.data.name
        })
    }
  }
}
</script>

<style scoped>
.col-centered{
    float: none;
    margin: 0 auto;
}
</style>
