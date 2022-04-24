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
              <h3 class="text-center mt-5">Register</h3>
              <form>
                <div class="form-group">
                  <label for="">Email</label>
                  <input
                    type="email"
                    class="form-control"
                    placeholder="Email"
                    v-model="form.email"
                  />
                </div>

                <div class="form-group mt-3">
                  <label for="">No Hp</label>
                  <input
                    type="text"
                    class="form-control"
                    placeholder="No Hp"
                    v-model="form.hp"
                  />
                </div>

                <div class="row mt-3">
                  <div class="col-sm-6">
                    <div class="form-group">
                      <label for="">Nama Pertama</label>
                      <input
                        type="text"
                        class="form-control"
                        placeholder="Nama Pertama"
                        v-model="form.firstname"
                      />
                    </div>
                  </div>
                  <div class="col-sm-6">
                    <div class="form-group">
                      <label for="">Nama Terakhir</label>
                      <input
                        type="text"
                        class="form-control"
                        placeholder="Nama Terakhir"
                        v-model="form.lastname"
                      />
                    </div>
                  </div>
                </div>

                <div class="row mt-3">
                  <div class="col-sm-6">
                    <div class="form-group">
                      <label for="">Tanggal Lahir</label>
                      <input
                        type="date"
                        class="form-control"
                        placeholder="Tanggal Lahir"
                        v-model="form.tgl_lahir"
                      />
                    </div>
                  </div>
                  <div class="col-sm-6">
                    <div class="form-group">
                      <label for="">Jenis Kelamin</label>
                      <select
                        name=""
                        id=""
                        class="form-select"
                        v-model="form.jenis_kelamin"
                      >
                        <option value="1">Laki-Laki</option>
                        <option value="2">Perempuan</option>
                      </select>
                    </div>
                  </div>
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
                      @click="register()"
                    >
                      Register
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
  name: "Register",
  data() {
    return {
      form: {
        email: "",
        hp: "",
        firstname: "",
        lastname: "",
        tgl_lahir: "",
        jenis_kelamin: "",
        password: "",
        grup: "member",
      },
    };
  },
  methods: {
    async register() {
      console.log(this.form);
      try {
        // const params = new URLSearchParams();
        // params.append("email", this.form.email);
        // params.append("hp", this.form.hp);
        // params.append("firstname", this.form.firstname);
        // params.append("lastname", this.form.lastname);
        // params.append("tgl_lahir", this.form.tgl_lahir);
        // params.append("jenis_kelamin", this.form.jenis_kelamin);
        // params.append("password", this.form.password);
        // params.append("grub", this.form.grub);

        axios
          .post(
            "http://202.157.184.201:8000/users",
            {
              email: this.form.email,
              hp: this.form.hp,
              firstname: this.form.firstname,
              lastname: this.form.lastname,
              tgl_lahir: this.form.tgl_lahir,
              jenis_kelamin: parseInt(this.form.jenis_kelamin),
              password: this.form.password,
              grup: this.form.grup,
            },
            {
              headers: {
                "Content-Type": "application/json",
                Accept: "*/*",
              },
            }
          )
          .then((response) => {
            console.log(response);
            if (response.data.status.kode == "success") {
              alert("Register Berhasil");
              this.$router.push("/");
            } else {
              alert("Register Gagal");
            }
          });
      } catch (error) {
        console.log(error);
      }
    },
  },
};
</script>