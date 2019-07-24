<template>
  <div>
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <router-link to="/">
        <a class="navbar-brand">Phonebook</a>
     </router-link>
      <div class="navbar-collapse">
        <ul class="navbar-nav mr-auto">
        </ul>
        <form class="form-inline my-2 my-lg-0">
          <div class="input-group">
            <div class="input-group-prepend">
              <span class="input-group-text">Search</span>
            </div>
            <input
              @input="searchContacts"
              v-model = "searchContactString"
              type="text"
              class="form-control"
              placeholder="Search...">
          </div>
        </form>
      <router-link to="/contact/0">
        <button
          type="button"
          class="btn btn-primary my-2 my-sm-0"
        >Add contact</button>
     </router-link>
      </div>
    </nav>

  <div id="app">
    <router-view/>
  </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data () {
    return {
      searchContactString: null
    }
  },
  methods: {
    searchContacts: function () {
      this.$root.$emit('searchContactsEmitted', this.searchContactString)
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
