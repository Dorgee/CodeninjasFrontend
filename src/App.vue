<template>
  <h1>Code Ninjas Accounts</h1>
  <Search />
  <AddAccount @hide-main="hideMain" @add-account="addAccount" />
  <MainAccount :accounts="accounts" v-if="showMainPage" />
</template>

<script>
import MainAccount from './components/MainAccount';
import Search from './components/Search';
import AddAccount from './components/AddAccount';
//import axios from 'axios';

export default {
  name: 'App',
  components: {
    MainAccount,
    Search,
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
      return data;
    },
    async addAccount(accountInformation) {
      console.log(accountInformation);

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

    //   axios
    //     .post('http://localhost:4000/account', {
    //       username: accountInformation.username,
    //       firstName: accountInformation.firstName,
    //       lastName: accountInformation.lastName,
    //     })
    //     .then((res) => {
    //       console.log(res);
    //     })
    //     .catch((err) => {
    //       console.log('something went wrong', err);
    //     });
    // },

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
