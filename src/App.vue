<script>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
import contacts from "./contacts.json";
export default {
  data() {
    return {
      contacts: contacts,  
      restOfContacts: contacts
    }
  },
  methods: {
    randomContact(){
      let randomNewContact = this.contacts[parseInt(Math.random()*this.contacts.length)];
      console.log(randomNewContact);
      this.contacts.push(randomNewContact);
    },
    sortByName(){
      this.contacts.sort(function(a,b) {
        return a.name > b.name
      });      
    },
    sortByPopularity(){
      this.contacts.sort(function(a,b) {
        return b.popularity - a.popularity;
      })
    },
    removeContact(contact){
      this.contacts=this.contacts.filter((t) => t.id !== contact.id)
    }
  },
  computed: {
    getContacts() {
      return contacts;
    }
  }
}
</script>

<template>
<h1>Contacts</h1>
<button @click="randomContact">Add Random Contact</button>
<button @click="sortByPopularity">Sort by popularity</button>
<button @click="sortByName">Sort by Name</button>
<table>
  <thead>
    <tr>
      <th>Picture</th>
      <th>Name</th>
      <th>Popularity</th>
      <th>Won an Oscar</th>
      <th>Won an Emmy</th>
      <th>Actions</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="contact in contacts" :key="contact.id" >
      <td><img style="width: 100px" :src="contact.pictureUrl" /></td>
      <td>{{contact.name}}</td>
      <td>{{contact.popularity.toFixed(2)}}</td>
      <td><img
              v-if="contact.wonOscar"
              src="https://github.githubassets.com/images/icons/emoji/unicode/1f3c6.png"
              alt="oscar trophy"
            /></td>
      <td><img
              v-if="contact.wonEmmy"
              src="https://github.githubassets.com/images/icons/emoji/unicode/1f3c6.png"
              alt="emmy trophy"
            /></td>
      <td><button @click="removeContact(contact)">Delete</button></td>
    </tr>
  </tbody>
</table>
 
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
