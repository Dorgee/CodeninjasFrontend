<template>
  <!-- <Search />
  <AddAccount /> -->
  <div class="search-bar">
    <input
      type="tel"
      name="search"
      id="search"
      placeholder="Search for a ninja"
      v-model="search"
    />
  </div>
  <!-- <div class="edit_user" v-if="isEditing">
    <form>
      <div class="form-group">
        <label for="userName">Username</label>
        <input
          type="text"
          class="form-control"
          placeholder="Username"
          v-model="username"
        />
      </div>
      <div class="form-group">
        <label for="firstName">Firstname</label>
        <input
          type="text"
          class="form-control"
          placeholder="Firstname"
          v-model="firstName"
        />
      </div>
      <div class="form-group">
        <label for="lastName">Lastname</label>
        <input
          type="text"
          class="form-control"
          placeholder="Lastname"
          v-model="lastName"
        />
      </div>
      <button type="submit" class="btn btn-primary edit" @click="editAccount">
        Edit
      </button>
    </form>
  </div> -->

  <table class="table table-hover table-dark">
    <thead>
      <tr>
        <th scope="col">Username</th>
        <th scope="col">First name</th>
        <th scope="col">Last name</th>
        <th scope="col">Scratch</th>
        <th scope="col">Roblox</th>
        <!-- <th scope="col">Edit</th> -->
        <th scope="col">Delete</th>
      </tr>
    </thead>
    <tbody>
      <tr :key="account._id" v-for="account in filteredAccounts">
        <td>
          {{ account.username }}
        </td>
        <td>{{ account.firstName }}</td>
        <td>{{ account.lastName }}</td>
        <td v-if="account.scratch.length > 0">
          <div :key="scratch._id" v-for="scratch in account.scratch">
            <p>username: {{ scratch.username }}</p>
            <p>Password: {{ scratch.password }}</p>
          </div>
        </td>
        <td v-else>
          <button type="button" class="btn btn-primary" @click="showScratch">
            Add Scratch Account
          </button>
          <Scratch v-if="showScratchAccount" :id="account._id" />
        </td>

        <td v-if="account.roblox.length > 0">
          <div :key="roblox._id" v-for="roblox in account.roblox">
            <p>username: {{ roblox.username }}</p>
            <p>Password: {{ roblox.password }}</p>
          </div>
        </td>
        <td v-else>
          <button type="button" class="btn btn-primary" @click="showRoblox">
            Add Roblox Account
          </button>
          <Roblox v-if="showRobloxAccount" :id="account._id" />
        </td>

        <!-- <td>
          <button @click="showForm">
            <i class="fas fa-edit"></i>
          </button>
        </td> -->
        <td>
          <button @click="$emit('delete-account', account._id)">
            <i class="fas fa-trash-alt"></i>
          </button>
        </td>
      </tr>
    </tbody>
  </table>
</template>

<script>
import Scratch from './Scratch';
import Roblox from './Roblox';

export default {
  name: 'MainAccount',
  components: {
    Scratch,
    Roblox,
  },
  props: {
    accounts: Array,
  },
  emits: ['delete-account', 'edit-acc'],
  data() {
    return {
      isEditing: false,
      username: '',
      firstName: '',
      lastName: '',
      showScratchAccount: false,
      showRobloxAccount: false,
      search: '',
    };
  },
  methods: {
    editAccount() {
      console.log(this.account.username);
      const editedInfo = {
        username: this.username,
        firstName: this.firstName,
        lastName: this.lastName,
      };
      this.$emit('edit-acc', editedInfo);
    },
    showForm() {
      this.isEditing = !this.isEditing;
    },
    showScratch() {
      this.showScratchAccount = !this.showScratchAccount;
      // window.scrollTo(0, 0);
    },
    addScratchAccount(accountInformation) {
      console.log(accountInformation);
    },
    showRoblox() {
      this.showRobloxAccount = !this.showRobloxAccount;
    },
  },
  computed: {
    filteredAccounts() {
      return this.accounts.filter((account) => {
        return account.firstName.toLowerCase().match(this.search.toLowerCase());
      });
    },
  },
};
</script>

<style scoped>
.table {
  margin-top: 20px;
}

.fas {
  color: #0d6efd;
}

.edit_user {
  height: 500px;
  width: 500px;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: white;
  border: 2px solid black;
  margin-left: auto;
  margin-right: auto;
}

.edit {
  margin-top: 1rem;
}

search {
  margin-left: 0.5rem;
}

.search-bar {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-wrap: wrap;
}
</style>
