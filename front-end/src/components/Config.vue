<template>
	<div v-if="loading">
		<img
			class="image"
			src="../../public/favicon.svg"
			alt
			width="120"
			height="120"
		/>
	</div>
	<div v-else>
		<v-app id="config">
			<span class="bg"></span>
			<v-content>
				<v-card class="mx-auto overflow-hidden">
					<v-app-bar class="headbg">
						<v-app-bar-nav-icon @click="drawer = true"></v-app-bar-nav-icon>
						<v-spacer />
						<center>
							<v-toolbar-title class="headfont">
								<strong>Fantasy Football 2020</strong>
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
						</v-list-item-group>
					</v-list>
				</v-navigation-drawer>
				<v-container absolute fluid>
					<v-row align="center" justify="center">
						<v-col cols="12" sm="8" md="4">
							<v-card class="card elevation-12">
								<v-toolbar color=" dark-blue darken-1" dark flat>
									<v-spacer></v-spacer>
									<v-toolbar-title>Game Configurations</v-toolbar-title>
									<v-spacer />
								</v-toolbar>
								<v-card-text>
									<v-form>
										<v-text-field
											v-model="gk"
											label="Number of goalkeepers"
											name="gk"
											type="text"
										/>

										<v-text-field
											v-model="mf"
											label="Number of mid-fielders"
											name="mf"
											type="text"
										/>

										<v-text-field
											v-model="df"
											label="Number of defenders"
											name="df"
											type="text"
										/>
										<v-text-field
											v-model="fwd"
											label="Number of forwards"
											name="fwd"
											type="text"
										/>
										<v-text-field
											v-model="mp"
											label="Penalty for more than 1 marquee player"
											name="mp"
											type="text"
										/>
									</v-form>
								</v-card-text>
								<v-card-actions>
									<v-spacer />
									<v-btn @click="send" rounded outlined class="btn-hover1" color="white">Send</v-btn>
									<v-btn @click="useDef" rounded outlined class="btn-hover" color="whitesmoke"
										>USE Default</v-btn
									>
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
	name: "Config",
	components: {
		Footer,
	},
	data() {
		return {
			drawer: false,
			mf: "",
			df: "",
			gk: "",
			mp: "",
			fwd: "",
			loading: true
		};
	},
	mounted() {
		this.$vuetify.theme.dark = true;
		axios
			.get("http://localhost:3000/getStatus")
			.then((res) => {
				var a = res.data;
				if (a.hasStarted === true) {
					if (a.lastPlayer.length > 0) {
						if (a.bidDone === true) this.$router.push("/players");
						else
							this.$router.push({
								name: "Player",
								query: { id: a.lastPlayer },
							});
					} else {
						this.$router.push("/register");
					}
				}
			})
			.finally(() =>
				this.sleep(500).then(() => {
					this.loading = false;
				})
			);
	},
	methods: {
		sleep(ms) {
			return new Promise((resolve) => setTimeout(resolve, ms));
		},
		useDef() {
			var a = {
				change: false,
			};
			axios.post("http://localhost:3000/startGame", a).then(() => {
				this.$router.push("/register");
			});
		},
		send() {
			var a = {
				change: true,
				mf: this.mf,
				df: this.df,
				gk: this.gk,
				mp: this.mp,
				fwd: this.fwd,
			};

			axios.post("http://localhost:3000/startGame", a).then(() => {
				this.$router.push("/register");
			});
		},
	},
};
</script>

<style>
.bg {
	width: 100%;
	height: 90%;
	position: absolute;
	top: 0;
	left: 0;
	opacity: 0.9;
	background: url("../../img/b4.png");
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
.btn-hover:hover{
  background: rgba(230, 144, 32, 0.539);

}
.btn-hover1:hover{
    background: rgba(6, 165, 6, 0.541);

}


.card {
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