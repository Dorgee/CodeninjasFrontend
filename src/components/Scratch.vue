<template>
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
  </form>
</template>

<script>
export default {
  name: 'Scratch',
  data() {
    return {
      userName: '',
      password: '',
    };
  },
};
</script>
