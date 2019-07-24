<template>
  <div class="hello">
    <h4>Contacts list</h4>

    <table class="table">
      <thead>
        <tr>
          <th scope="col">Contact name</th>
          <th scope="col">Phone(s)</th>
          <th scope="col">Action</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(contact, index) in contacts" :key="`contact-${index}`">
          <th scope="row">{{ contact.name }}</th>
          <td></td>
          <td>
            <div>
              <b-dropdown
                variant="primary"
                class="m-2"
              >
                <template slot="button-content">
                  <font-awesome-icon icon="cog" />
                </template>
                <b-dropdown-item
                  @click="editContact(index)"
                  >Edit contact</b-dropdown-item>
                <b-dropdown-item
                  @click="deleteContact(contact.id)"
                >Delete contact</b-dropdown-item>
              </b-dropdown>
             </div>
           </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: 'Main',
  data () {
    return {
      contacts: []
    }
  },
  methods: {
    updateContacts (search = '') {
      this.axios.get('/contacts/' + search)
        .then((response) => {
          this.contacts = response.data
        })
    },
    deleteContact (index) {
      this.axios.delete('/contact/' + this.contacts[index].id)
        .then((response) => {
          this.$delete(this.contacts, index)
        })
    },
    editContact (contactId) {
      this.$router.push('/contact/' + contactId)
    }

  },

  created () {
    this.updateContacts()
  },
  mounted () {
    this.$root.$on('searchContactsEmitted', (text) => {
      this.updateContacts(text)
    })
  }
}
</script>

<style scoped>
.vh-100 {
    min-height: 100vh;
}
</style>
