<template>
  <div class="add">
    <h3>Add Account</h3>
    <button @click="toggleAddAccount">
      <i v-if="!isVisible" class="fas fa-user-plus"></i>
      <i v-else class="fas fa-times"></i>
    </button>
  </div>

  <div class="add_user" v-if="isVisible">
    <form>
      <div class="form-group">
        <label for="userName">Username</label>
        <input
          type="text"
          class="form-control"
          placeholder="Username"
          v-model="userName"
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
      <button type="submit" class="btn btn-primary" @click="addAccount">
        Add
      </button>
    </form>
  </div>
</template>

<script>
export default {
  name: 'AddAccount',
  emits: ['hide-main', 'add-account'],
  data() {
    return {
      isVisible: false,
      userName: '',
      firstName: '',
      lastName: '',
    };
  },
  methods: {
    toggleAddAccount() {
      this.isVisible = !this.isVisible;
      const visible = this.isVisible;
      this.$emit('hide-main', visible);
    },
    addAccount() {
      const accountInformation = {
        username: this.userName,
        firstName: this.firstName,
        lastName: this.lastName,
      };

      this.$emit('add-account', accountInformation);
    },
  },
};
</script>

<style scoped>
.fas {
  color: #0d6efd;
}

.add {
  display: flex;
  justify-content: flex-end;
  margin-right: 3rem;
}

h3 {
  padding-right: 1rem;
}

.add_user {
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

.btn {
  margin-top: 2rem;
}
</style>
