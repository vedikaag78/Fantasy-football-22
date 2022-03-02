<template>
	<body>
		<main class="main">
			<div class="signup-section">
				<div class="signup-box">
					<h1 class="main-heading">Fantasy <br>Football</h1>
					<p class="body-text">Let's begin the game, shall we?</p>

					<router-link to="/config" tag="button" class="signup-button"
						>Play</router-link
					>
				</div>
			</div>
		</main>
	</body>
</template>

<script>
export default {
	name: "Home",
	data() {
		return {};
	},
};
</script>

<style scoped>
/* CSS reset ==============================================*/
*,
*::after,
*::before {
	box-sizing: inherit;
	margin: 0;
	padding: 0;
}

body {
	box-sizing: border-box;
	position: relative;
}

html {
	/* formula: 1 rem = 10px; 10px/16px = 62.5% */
	font-size: 62.5%;
}

/* Typography ================================================*/

* {
	color: #eee;
	font-family: "Open Sans", sans-serif;
}
@import url("http://fonts.cdnfonts.com/css/pf-tempesta-seven");
@import url('https://fonts.googleapis.com/css2?family=Questrial&family=Roboto:wght@100&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Bangers&family=Questrial&family=Roboto:wght@100&display=swap');
/* Signup heading */
.main-heading {
	padding-top: 2.5rem ;
    color: rgb(168, 18, 18);
	font-family: 'Bangers', cursive;
    /* font-family: 'Questrial', sans-serif;
    font-family: 'Roboto', sans-serif; */
	/* font-family: 'Questrial', sans-serif;
    font-family: 'Roboto', sans-serif; */
	/* font-family: "PF Tempesta Seven", sans-serif;
	font-family: "PF Tempesta Seven Extended", sans-serif;
	font-family: "PF Tempesta Seven Condensed", sans-serif;
	font-family: "PF Tempesta Seven Compressed", sans-serif; */
	font-size: 5.2rem;
	padding-bottom: 2.5rem;
	width: 40rem;
}
/* Signup text */
.body-text {
	color: rgb(16, 29, 104);
	font-family: 'Questrial', sans-serif;
    font-family: 'Roboto', sans-serif;
	font-family: "PF Tempesta Seven", sans-serif ;
	font-size: 1.8rem;
	font-weight: 300;
	line-height: 2rem;
	padding-bottom: 2.5rem;
}

/* Components ================================================*/

/* Signup button */
.signup-button {
	background-color: rgb(14, 38, 88);
	border: 1px solid rgb(8, 16, 44);
	border-radius: 6rem;
	color: #eee;
	font-size: 1.5rem;
	overflow: hidden;
	padding: 1rem 2rem;
	position: relative;
	transition: all 0.2s ease-in-out;
	z-index: 10;
}

.signup-button:hover {
	color: #272829;
}

.signup-button::before {
	background-color: #eee;
	content: "";
	height: 100%;
	left: 0;
	position: absolute;
	top: 0;
	transform: scaleX(0);
	transition: all 0.2s ease-in-out;
	width: 100%;
	z-index: -1;
}

.signup-button:hover::before {
	transform: scaleX(1);
}

/* Layout ================================================*/

.main {
	align-items: center;
	background: linear-gradient(to right bottom, #272829, #37383b, #272829);
	background-image: url("https://i.gifer.com/qhn.gif") !important;
	/* background-image: url("../../public/homebg.mp4") !important; */
    background-position-x: -30em;
	background-size: cover;
	display: flex;
	flex-direction: row;
	height: 100vh;
	position: relative;
	width: 100%;
}

/* Signup section (on left side) */
.signup-section {
	align-items: center;
	display: flex;
	flex-direction: column;
	height: 100%;
	justify-content: center;
  margin-left: 49%;
}

/* Container for heading, text, and button  */
.signup-box {
 
	border-radius: 8px;
	/* border: solid rgb(75, 74, 74) 1px; */
	transform: translateY(1em);
	background: rgba(241, 211, 211, 0.486);
	border-bottom: solid rgb(38, 56, 70) 8px;
	box-shadow: #2d4153 5px 5px 15px;
	text-align: center;
	backdrop-filter: blur(4px);
	width: 100%;
	height: 55%;
	
}



/* Videos ==============================================================*/

/* Specifically targeting the <video> element */
.video__container {
	height: auto;
	min-height: 100%;
	object-fit: cover;
	width: 100%;
}

/* Responsive ============================================================*/

/* Tablet */
@media only screen and (max-width: 48em) {
	/* CSS Reset */

	html {
		font-size: 56.25%;
	}

	/* Typography */

	/* Signup heading */
	.main-heading {
		width: 100%;
	}

	/* Layout */

	.main {
		flex-direction: column-reverse;
		height: 100%;
	}

	/* Signup section (on left side) */
	.signup-section {
		height: 100%;
		margin-left: 0;
		width: 100%;
	}

	/* Container for heading, text, and button  */
	.signup-box {
		height: 100%;
		padding: 3rem 2rem;
		text-align: center;
	}

	/* Showbox cube section (on right side) */
	.cube__section {
		height: 100vh;
		width: 100%;
	}
}

/* Mobile */
@media only screen and (max-width: 22.5em) {
	/* Typography */

	/* Signup text */
	.body-text {
		font-size: 1.8rem;
		line-height: 2.8rem;
	}

	/* Layout */

	/* Signup section (on left side) */
	.signup-section {
		height: 100%;
		margin-left: 0;
		width: 100%;
	}

	/* Container for heading, text, and button  */
	.signup-box {
		height: 100%;
		padding: 3rem;
		padding-top: 1rem;
		text-align: center;
	}

	/* Showbox cube section (on right side) */
	.cube__section {
		height: 60vh;
		width: 100%;
	}

	/* The cube outer container */
	.cube {
		height: 15rem;
		perspective: 60rem;
		width: 15rem;
	}

	/* The cube's inner container */
	.cube__container {
		transform: translateZ(-7.5rem);
	}

	/* This will target every single side of the cubes */
	.cube__face {
		height: 15rem;
		width: 15rem;
	}

	/* This will target an individual side of the cube */
	.cube__face--front {
		transform: rotateY(0deg) translateZ(7.5rem);
	}
	.cube__face--back {
		transform: rotateY(180deg) translateZ(7.5rem);
	}
	.cube__face--left {
		transform: rotateY(-90deg) translateZ(7.5rem);
	}
	.cube__face--right {
		transform: rotateY(90deg) translateZ(7.5rem);
	}
	.cube__face--top {
		transform: rotateX(90deg) translateZ(7.5rem);
	}
	.cube__face--bottom {
		transform: rotateX(-90deg) translateZ(7.5rem);
	}
}

/* Animation ============================================================*/

@keyframes rotationBox {
	0% {
		transform: rotate3d(0, 0, 0, 0deg);
	}
	25% {
		transform: rotate3d(0, 1, 1, 90deg);
	}
	50% {
		transform: rotate3d(1, 0, 1, 180deg);
	}
	75% {
		transform: rotate3d(1, 1, 0, 240deg);
	}
	100% {
		transform: rotate3d(1, 1, 1, 360deg);
	}
}
</style>