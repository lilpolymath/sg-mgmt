<template>
    <div class="login">
      <div>
        <form @submit.prevent="submit">
        <!-- <form> -->
          <div>
            <label for="Email">Email:</label>
            <input type="text" name="email" v-model="form.email" />
          </div>
          <div>
            <label for="password">Password:</label>
            <input type="password" name="password" v-model="form.password" />
          </div>
          <button type="submit">Submit</button>
        </form>
        <!-- <p v-if="showError" id="error">Email or Password is incorrect</p> -->
      </div>
    </div>
  </template>


<script>
import { mapActions } from "vuex";

export default {
  name: "LogIn",
  components: {},
  data() {
    return {
      form: {
        email: "",
        password: "",
      },
      showError: false
    };
  },
  methods: {
    ...mapActions(["LogIn"]),
    async submit() {
      console.log("submit");
      // const User = new FormData();
      // User.append("username", this.form.email);
      // User.append("password", this.form.password);

      const User = {
        email: this.form.email,
        password: this.form.password
      }
      
      try {
          console.log("try")
          await this.LogIn(JSON.stringify(User));
          // this.$router.push("/posts");
          // this.showError = false
          console.log("success")
      } catch (error) {
        this.showError = true
      }
    },
  },
};
</script>

<style scoped>
* {
  box-sizing: border-box;
}
label {
  padding: 12px 12px 12px 0;
  display: inline-block;
}
button[type=submit] {
  background-color: #4CAF50;
  color: white;
  padding: 12px 20px;
  cursor: pointer;
  border-radius:30px;
}
button[type=submit]:hover {
  background-color: #45a049;
}
input {
  margin: 5px;
  box-shadow:0 0 15px 4px rgba(0,0,0,0.06);
  padding:10px;
  border-radius:30px;
}
#error {
  color: red;
}
</style>


  