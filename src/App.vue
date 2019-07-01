<template>
  <div id="app" class="container">
    <header>
      <div class="row">
        <div class="col-sm-8 m-auto">
          <div id="header-contact">
              <small>Showing {{search.length}}</small>
              <h2>Contact List</h2>
              <input id="search" type="text" class="form-control" v-model="query" placeholder="Search in contacts">
          </div>
        </div>
      </div>
    </header>
    <app-contacts :contacts="search"></app-contacts>
  </div>
</template>

<script>
import ContactsComponent from './components/contacts'
import contactsList from './assets/contacts.json'

export default {
  name: 'app',
  components: {
    'app-contacts': ContactsComponent
  },
  data () {
    return {
      contacts: contactsList,
      query: ''
    }
  },
  mounted () {
    console.log(this.contacts)
  },
  computed: {
    search: {
      get: function () {
        return this.contacts.filter(contact => {
          let query = this.query.toLowerCase()
          return  contact.firstname.toLowerCase().match(query) || contact.lastname.toLowerCase().match(query) || contact.email.find( email => {return email.toLowerCase().match(query)}) || contact.phoneNumber.find( phone => {return phone.match(query)})
        })
      }
    }
  }
}
</script>

<style lang="scss">
#app {
  font-family: 'Nunito', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 20px;
}
header{
    position: fixed;
    top: 20px;
    left: 50%;
    width: 82%;
    transform: translateX(-50%);
    z-index: 2;
}
#header-contact{
  display: flex;
  align-items: center;
  padding: 20px;
  background: rgba(2, 1, 6, .9);
  border-bottom: 1px solid rgba(46, 46, 48, 0.89);
  border-top-left-radius: 5px;
  border-top-right-radius: 5px;
  h2{
    color: #fff;
    font-weight: bold;
    text-align: left;
    min-width: 200px;
    margin: 0;
  }
  small{
    position: absolute;
    bottom: 6px;
    left: 38px;
    color: #2098D1;
  }
}
@media(max-width: 767px) {
  header{
    .col-sm-8{
      padding: 0;
    }
    #header-contact{
      display: block;
      small{
        left: auto;
        right: 20px;
        bottom: 66px;
      }
    }
  }
}
</style>
