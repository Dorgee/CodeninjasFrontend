<template>
  <!-- <Search />
  <AddAccount /> -->
  <div class="edit_user" v-if="isEditing">
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
  </div>
  <div><Scratch v-if="showScratchAccount" /></div>
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
      <tr :key="account._id" v-for="account in accounts">
        <td>
          {{ account.username }}
        </td>
        <td>{{ account.firstName }}</td>
        <td>{{ account.lastName }}</td>
        <td>
          <p>Username: ScratchKat123</p>
          <p>Password: mahoganycn</p>
          <button type="button" class="btn btn-primary" @click="showScratch">
            Add Scratch Account
          </button>
        </td>

        <td>
          <p>Username: ScratchKat123</p>
          <p>Password: mahoganycn</p>
          <button type="button" class="btn btn-primary">
            Add Roblox Account
          </button>
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
// import Search from './Search';
// import AddAccount from './AddAccount';
import Scratch from './Scratch';

export default {
  name: 'MainAccount',
  components: {
    Scratch,
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
</style>
