<template>
  <h1>Code Ninjas Accounts</h1>

  <AddAccount @hide-main="hideMain" @add-account="addAccount" />
  <MainAccount
    :accounts="accounts"
    v-if="showMainPage"
    @delete-account="deleteAccount"
    @edit-acc="editAccount"
  />
</template>

<script>
import MainAccount from './components/MainAccount';
import AddAccount from './components/AddAccount';
//import axios from 'axios';

export default {
  name: 'App',
  components: {
    MainAccount,
    AddAccount,
  },
  data() {
    return {
      accounts: [],
      showMainPage: true,
    };
  },
  methods: {
    async fetchAccounts() {
      const res = await fetch('http://localhost:4000/account/all');
      const data = await res.json();
      //  console.log(data[2].scratch[0].username);
      return data;
    },
    async addAccount(accountInformation) {
      //console.log(accountInformation);

      const res = await fetch('http://localhost:4000/account', {
        method: 'POST',
        headers: {
          'Content-type': 'application/json',
        },
        body: JSON.stringify(accountInformation),
      });
      console.log(res.json());
      const data = await res.json();
      console.log('data: ', data);
    },
    async deleteAccount(id) {
      if (confirm('Are you sure buddy?')) {
        const res = await fetch(`http://localhost:4000/account/${id}`, {
          method: 'DELETE',
        });
        console.log(res);
        location.reload();
      }
    },
    async editAccount(editedInfo) {
      const res = await fetch('http://localhost:4000/account', {
        method: 'PATCH',
        headers: {
          'Content-type': 'application/json',
        },
        body: JSON.stringify(editedInfo),
      });
      console.log(res.json());
      const data = await res.json();
      console.log('data: ', data);
    },

    hideMain(visible) {
      this.showMainPage = !visible;
    },
  },
  async created() {
    this.accounts = await this.fetchAccounts();
  },
};
</script>

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
