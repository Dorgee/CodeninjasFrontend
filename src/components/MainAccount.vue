<template>
  <!-- <Search />
  <AddAccount /> -->
  <table class="table table-hover table-dark">
    <thead>
      <tr>
        <th scope="col">Username</th>
        <th scope="col">First name</th>
        <th scope="col">Last name</th>
        <th scope="col">Scratch</th>
        <th scope="col">Roblox</th>
        <th scope="col">Edit</th>
        <th scope="col">Delete</th>
      </tr>
    </thead>
    <tbody>
      <tr :key="account.id" v-for="account in accounts">
        <td>{{ account.username }}</td>
        <td>{{ account.firstName }}</td>
        <td>{{ account.lastName }}</td>
        <td>
          <button type="button" class="btn btn-primary">Scratch Account</button>
        </td>
        <td>
          <button type="button" class="btn btn-primary">Roblox Account</button>
        </td>
        <td>
          <button><i class="fas fa-edit"></i></button>
        </td>
        <td>
          <button><i class="fas fa-trash-alt"></i></button>
        </td>
      </tr>
    </tbody>
  </table>
</template>

<script>
// import Search from './Search';
// import AddAccount from './AddAccount';
export default {
  name: 'MainAccount',
  props: {
    accounts: Array,
  },
  data() {
    return {};
  },
  methods: {},
  components: {},
};
</script>

<style scoped>
.table {
  margin-top: 20px;
}

.fas {
  color: #0d6efd;
}
</style>
