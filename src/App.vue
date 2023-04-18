<template>
  <div id="app">
    <h1>IronContacts</h1>
    <div id="btns">
    <button class="addBtn" @click="addRandomContact">Add Random Contact</button>
    <button @click="sortByName">Sort by Name</button>
    <button @click="sortByPopularity">Sort by Popularity</button>
    </div>
    <table>
      <thead>
        <tr>
          <th>Picture</th>
          <th>Name</th>
          <th>Popularity</th>
          <th>Won an<br> Oscar</th>
          <th>Won an<br>Emmy</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(contact, index) in contacts" :key="contact.id">
          <td><img :src="contact.pictureUrl" :alt="contact.name" /></td>
          <td>{{ contact.name }}</td>
          <td>{{ contact.popularity.toFixed(2) }}</td>
          <td v-if="contact.wonOscar"><span class="trophy">🏆</span></td>
          <td v-else></td>
          <td v-if="contact.wonEmmy"><span class="trophy">✨</span></td>
          <td v-else></td>
          <td><button @click="removeContact(index)">Delete</button></td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import contacts from "./contacts.json";

export default {
  name: "App",
  data() {
    return {
      contacts: contacts.slice(0, 5),
      remainingContacts: contacts.slice(5),
    };
  },
  methods: {
    addRandomContact() {
      if (this.remainingContacts.length > 0) {
        const randomIndex = Math.floor(Math.random() * this.remainingContacts.length);
        const randomContact = this.remainingContacts.splice(randomIndex, 1)[0];
        this.contacts.push(randomContact);
      }
    },
    removeContact(index) {
      this.contacts.splice(index, 1);
    },
    sortByName() {
      this.contacts.sort((a, b) => a.name.localeCompare(b.name));
    },
    sortByPopularity() {
      this.contacts.sort((a, b) => b.popularity - a.popularity);
    },

  },
};
</script>

<style>

#app {
  width: 100vw;
  text-align: center;
  display: flex;
  flex-direction: column;
  place-content: center;
}

#btns {
  position: fixed;
  top: 10px;
  right: 50px;
}

img {
  width: 100px;
  height: auto;
}

tr {
  padding: 10px;
}

td {
  padding: 10px;
}

th {
  font-size: 20px;
}
</style>
