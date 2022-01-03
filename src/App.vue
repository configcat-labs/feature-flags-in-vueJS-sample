<template>
	<div id="app">
		<button class='btn' @click='getUserAgeFeatureStatus'>
			Calculate Age
		</button>
		
		<p v-if='!userAgeFeature && !loading' class='text'>Sorry, This feature has been disabled by the Admin</p>
		<p v-else-if="error">{error}</p>

		<div v-else-if='userAgeFeature'>
			<p class='text'>Calculate your age below by providing your year of birth</p>
			<input
				type='number'
				v-model='birthYear'
			/>
			<button class='btn btn-calculate' @click='calcAge'>
				Calculate
			</button>

			<p v-if='age'>You are {{ age }} years old</p>
		</div>
	</div>
</template>

<script>
import * as configCat from "configcat-js"

export default {
	name: 'App',
	data() {
		return {
			userAgeFeature: null,
			error: null,
			birthYear: '',
			age: '',
			loading: true
		}
	},
	methods: {
		// Get feature status from ConfigCat
		async getUserAgeFeatureStatus() {
			try {
				let configCatClient = configCat.createClient(
					process.env.VUE_APP_CONFIGCAT_SDK
				);
				const res = await configCatClient.getValueAsync(
					"calculateuseragefeature",
					false
				);
				this.userAgeFeature = res
			} catch (err) {
				this.error = err.message
			}
			this.loading = false;
		},
		// Calculate age Feature
		calcAge() {
			const age = 2021 - this.birthYear;
			this.age = age;
			this.birthYear = '';
		}
	}
}
</script>

<style>
body {
	margin: 0;
}

#app {
	text-align: center;
	background-image: linear-gradient(110deg, #1c3863 0%, #01183b 100%);
	min-height: 100vh;
	display: flex;
	flex-direction: column;
	justify-content: center;
	align-items: center;
}

.btn {
	color: rgb(16, 82, 54);
	background-color: #FFF;
	border: none;
	padding: 13px 25px;
	border-radius: 15px;
	font-size: 1.2rem;
	cursor: pointer;
	font-weight: 600;
}

.btn:hover {
	background-color: rgb(16, 82, 54);
	color: #FFF;
}

.btn:focus-visible,
input:focus-visible {
	outline: none;
}

.btn-calculate {
	padding: 10px 25px;
	margin-left: 8px;
	border-radius: 8px;
}

input {
	padding: 10px 25px;
	font-size: 1.2rem;
	border-radius: 8px;
	border: none;
}

.text {
	font-size: 1.5em;
	color: #FFF;
}
</style>
