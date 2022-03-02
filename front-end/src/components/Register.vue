

<template>
  <div v-if="loading">
    <img class="image" src="../../public/favicon.svg" alt width="120" height="120" />
  </div>
  <div v-else>
    <v-app id="config">
      <span class="bg"></span>
      <v-content>
        <v-card class="mx-auto overflow-hidden ">
          <v-app-bar class="headbg">
            <v-app-bar-nav-icon @click="drawer = true"></v-app-bar-nav-icon>
            <v-spacer />
            <center>
              <v-toolbar-title class="headfont">
                <strong>Fantasy Football 2022</strong>
              </v-toolbar-title>
            </center>
            <v-spacer />
          </v-app-bar>
        </v-card>

        <v-navigation-drawer v-model="drawer" absolute temporary>
          <v-list nav dense>
            <v-list-item-group active-class="deep-purple--text text--lighten-2">
              <router-link tag="span" to="/">
                <v-list-item>
                  <v-list-item-icon>
                    <v-icon>mdi-home</v-icon>
                  </v-list-item-icon>
                  <v-list-item-title>Home</v-list-item-title>
                </v-list-item>
              </router-link>
              <router-link tag="span" to="/players">
                <v-list-item>
                  <v-list-item-icon>
                    <v-icon>mdi-soccer</v-icon>
                  </v-list-item-icon>
                  <v-list-item-title>CONTINUE AUCTION</v-list-item-title>
                </v-list-item>
              </router-link>
            </v-list-item-group>
          </v-list>
        </v-navigation-drawer>
        <v-container absolute fluid>
          <v-row align="center" justify="center">
            <v-col cols="12" sm="8" md="4">
              <v-card class="elevation-12 style-card">
                <v-toolbar color="darken-1" dark flat>
                  <v-spacer></v-spacer>
                  <v-toolbar-title>Register Teams</v-toolbar-title>
                  <v-spacer />
                </v-toolbar>
                <v-card-text>
                  <v-form>
                    <v-text-field v-model="name" label="Team Name" name="name" type="text" />

                    <v-text-field v-model="money" label="Base Price" name="money" type="text" />
                  </v-form>
                </v-card-text>
                <v-card-actions>
                  <v-spacer />
                  <v-btn class="btn-hover" @click="register" outlined rounded color="whitesmoke">Register</v-btn>
                  <v-btn class="btn-hover1" @click="auction" outlined rounded color="white">START</v-btn>
                </v-card-actions>
              </v-card>
            </v-col>
          </v-row>
        </v-container>
      </v-content>
      <Footer />
    </v-app>
  </div>
</template>

<script>
import axios from "axios";
import Footer from "./layout/Footer";

export default {
  name: "Register",
  components: {
    Footer
  },
  data() {
    return {
      drawer: false,

      team: "",
      money: "",
      error: "",
      loading: true
    };
  },
  created() {
    this.$vuetify.theme.dark = true;
    this.sleep(500).then(() => {
      this.loading = false;
    });
  },
  methods: {
    sleep(ms) {
      return new Promise(resolve => setTimeout(resolve, ms));
    },
    register() {
      const team = {
        name: this.name,
        money: this.money
      };
      axios.post("http://localhost:3000/addTeam", team).then(
        res => {
          if (res.status === 200) {
            if (res.data.done === false) alert(`ERROR! ${res.data.message}`);
            else {
              alert(`Sucesss! ${res.data.message}`);
              location.reload();
            }
          }
        },
        err => {
          console.log(err.response);
          this.error = err.response.data.error;
        }
      );
    },
    auction() {
      axios.post("http://localhost:3000/loadCsv").then(() => {
        this.$router.push("/players");
      });
    }
  }
};
</script>


<style scoped>

.btn-hover:hover{
  background: rgba(230, 144, 32, 0.539);

}
.btn-hover1:hover{
    background: rgba(6, 165, 6, 0.541);

}





.bg {
  width: 100%;
  height: 90%;
  position: absolute;
  top: 0;
  left: 0;
  opacity: 2.5;
  background: url("../../img/b4.png") no-repeat;
  background-size: cover;
  background-color: blue;
  transform: scale(1.1);
}
#inspire {
  height: 100%;
  width: 100%;
  overflow: auto;
  padding-right: 20px;
}
@import url("http://fonts.cdnfonts.com/css/pf-tempesta-seven");
@import url('https://fonts.googleapis.com/css2?family=Questrial&family=Roboto:wght@100&display=swap');
.headfont{
   font-family: "PF Tempesta Seven", sans-serif;
	font-family: "PF Tempesta Seven Extended", sans-serif;
	font-family: "PF Tempesta Seven Condensed", sans-serif;
	font-family: "PF Tempesta Seven Compressed", sans-serif; 
}
.headbg{
  background: rgba(177, 226, 87, 0.685) !important;
  backdrop-filter: blur(5px);

}

.style-card{
  backdrop-filter: blur(8px);
	background: rgba(70, 68, 68, 0.8) !important;
}
.image {
  position: absolute;
  top: 50%;
  left: 50%;
  width: 120px;
  height: 120px;
  margin: -60px 0 0 -60px;
  webkit-animation: spin 4s linear infinite;
  -moz-animation: spin 4s linear infi-nite;
  animation: spin 4s linear infinite;
}
@-moz-keyframes spin {
  100% {
    -moz-transform: rotate(360deg);
  }
}
@-webkit-keyframes spin {
  100% {
    -webkit-transform: rotate(360deg);
  }
}
@keyframes spin {
  100% {
    -webkit-transform: rotate(360deg);
    transform: rotate(360deg);
  }
}
</style>
