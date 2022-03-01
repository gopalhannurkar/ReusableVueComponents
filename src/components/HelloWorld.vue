<template>
  <div v-if="success">
    <p>Welcome {{ userName }}</p>

    <button class="cust_btn" type="button" v-on:click="login(1)">Logout</button>
  </div>
  <div
    v-else
    style="
      justify-content: center;
      display: flex;
      flex-direction: column;
      align-items: center;
    "
  >
    <div
      style="
        justify-content: center;
        align-items: center;
        display: flex;
        flex-direction: column;
        margin: auto;
      "
    >
      <div class="login-card">
        <p style="colo: #4a4544; font-weight: 500; font-size: 18px">
          Member Login
        </p>
        <form>
          <textBoxComponent
            v-model.trim="userName"
            placeholder="UserName"
            InputType="text"
            icon="person"
            :v="$v.userName"
            validationcheck="yes"
          />

          <textBoxComponent
            v-model="password"
            placeholder="Password"
            InputType="password"
            icon="lock"
          />

          <div
            style="
              justify-content: space-between;
              display: flex;
              align-items: center;
              margin-top: 20px;
            "
          >
            <checkBoxComponent
              v-model="isChecked"
              style="
                margin-right: 40px;
                color: #b1b1b4;
                font-weight: 500;
                font-size: 16px;
              "
            >
              Remember Me
            </checkBoxComponent>
            <p
              style="
                margin: 0px;
                padding: 0px;
                color: #b1b1b4;
                font-style: italic;
                font-weight: 500;
                font-size: 16px;
              "
            >
              Forget Password?
            </p>
          </div>
          <div
            style="justify-content: flex-start; display: flex; margin-top: 20px"
          >
            <button class="cust_btn" type="button" v-on:click="login">
              Login
            </button>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import textBoxComponent from "./textBoxComponent.vue";
import checkBoxComponent from "./checkBoxComponent.vue";
import { email } from "vuelidate/lib/validators";
export default {
  validations: {
    userName: { email },
  },
  components: { textBoxComponent, checkBoxComponent },
  data: () => ({
    userName: "",
    password: "",
    isChecked: false,
    success: false,
  }),
  methods: {
    login(incmg) {
      if (incmg === 1) {
        this.success = false;
        this.userName = "";
        this.password = "";
        this.isChecked = false;
        return;
      }
      console.log(" this.$v.frstnmeInd", this.$v.userName.$error);
      if (!this.userName.length || !this.password.length) {
        alert("Please Enter UserName and Password");
        return;
      }
      if (this.$v.userName.$error) {
        alert("Please Enter Valid Email ID");
        return;
      }
      let data = {
        username: this.userName,
        password: this.password,
      };

      // login credentials

      //       {
      //     "email": "eve.holt@reqres.in",
      //     "password": "cityslicka"
      // }

      console.log(this.userName, "userName");
      console.log(this.password, "password");
      console.log(this.isChecked, "isChecked");
      axios
        .post("https://reqres.in/api/login", data)
        .then((response) => {
          console.log(response, "response of POST");
          this.success = true;
        })
        .catch(function (error) {
          console.log("error of POST", error.response.data.error);
          alert(error.response.data.error);
        });
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.login-card {
  height: auto;
  background: #fff;
  padding: 20px;
  box-shadow: 0 4px 10px 0 rgb(0 0 0 / 10%);
}
.cust_btn {
  background-color: orange;
  color: #fff;
  font-weight: bold;
  font-size: 15px;
  padding: 10px 50px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}
</style>
