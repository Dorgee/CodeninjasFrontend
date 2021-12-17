<template>
  <div class="f">
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
        <label for="firstName">Password</label>
        <input
          type="text"
          class="form-control"
          placeholder="Password"
          v-model="password"
        />
      </div>
      <br />
      <button type="submit" class="btn btn-primary" @click="addAccount">
        Add Account
      </button>
      <!-- <button type="button" class="btn btn-danger">Delete Account</button> -->
    </form>
  </div>
</template>

<script>
export default {
  name: 'Scratch',
  props: {
    id: String,
  },
  data() {
    return {
      userName: '',
      password: '',
    };
  },
  methods: {
    async addAccount() {
      const accountInformation = {
        username: this.userName,
        password: this.password,
      };
      const res = await fetch(
        `http://localhost:4000/account/${this.id}/scratch`,
        {
          method: 'POST',
          headers: {
            'Content-type': 'application/json',
          },
          body: JSON.stringify(accountInformation),
        }
      );
      console.log(res.json());
      const data = await res.json();
      console.log('data: ', data);
    },
  },
};
</script>

<style scoped>
.f {
  display: flex;
  justify-content: center;
  margin-top: 1rem;
}

/* .f form {
  width: 400px;
  height: 250px;
  background-color: white;
  border: 2px solid black;
  padding: 30px 30px 30px 30px; 
} */
/* .btn {
  margin-right: 1rem;
} */
</style>
