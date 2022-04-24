<template>
  <div class="container">
    <div class="d-flex justify-content-center">
      <div class="card shadow p-4 rounded">
        <div class="card-body">
          <div class="row">
            <div class="col-md-6">
              <img src="../assets/image/gambar.png" class="img-fluid" />
            </div>
            <div class="col-md-6">
              <form>
                <h3 class="text-center mt-5">Login</h3>
                <div class="form-group">
                  <label for="">Username</label>
                  <input
                    type="text"
                    class="form-control"
                    placeholder="Username"
                    v-model="form.username"
                  />
                </div>

                <div class="form-group mt-3">
                  <label for="">Password</label>
                  <input
                    type="password"
                    class="form-control"
                    placeholder="Password"
                    v-model="form.password"
                  />
                </div>
                <div class="form-group mt-3 mb-5">
                  <div class="d-grid gap-2">
                    <button
                      class="btn btn-success"
                      type="button"
                      @click="login"
                    >
                      Login
                    </button>
                  </div>
                </div>
              </form>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style>
.card {
  width: 60rem;
  margin-top: 5rem;
  margin-bottom: 5rem;
  border: none;
}
</style>

<script>
import axios from "axios";

export default {
  name: "Login",
  data() {
    return {
      form: {
        username: "",
        password: "",
      },
    };
  },
  methods: {
    async login() {
      //   console.log(this.form);
      try {
        const params = new URLSearchParams();
        params.append("username", this.form.username);
        params.append("password", this.form.password);

        let result = await axios.post(
          "http://202.157.184.201:8000/login",
          params,
          {
            headers: {
              "Content-Type": "application/x-www-form-urlencoded",
            },
          }
        );

            console.log(result);

        if (result.data.status.kode == "success") {
          localStorage.setItem("token", result.data.token);
          this.$router.push("/home");
        } 
      } catch (error) {
          console.log(error);
          
      }
    },
  },
};
</script>