<template>
  <main id="main">
    <button class="btn">
      Calculate Age
    </button>

    <FeatureWrapper>

      <div>
      <p class="text">Calculate your age below by providing your year of birth</p>
      <input type='number' v-model='appData.birthYear' />
      <button class='btn btn-calculate' @click='calculateUserAge()'>
        Calculate
      </button>

      <p>You are {{ appData.age }} years old</p>
    </div>

      <template #else>
        Sorry, This feature has been disabled by the Admin
      </template>

    </FeatureWrapper>



  </main>
</template>

<script setup lang="ts">
import { reactive } from 'vue';


const appData = reactive({
  userAgeFeature: null,
  error: null,
  birthYear: 0,
  age: 0,
});

const calculateUserAge = () => {
  appData.age = new Date().getFullYear() - appData.birthYear;
  appData.birthYear = 0;
}

</script>

<style scoped>
#main {
	text-align: center;
	 background-image: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
	min-height: 100vh;
	display: flex;
	flex-direction: column;
	justify-content: center;
	align-items: center;
}

.btn {
	color: rgb(16, 82, 54);
	  background-color: royalblue;
	border: none;
	 padding: 8px 16px;
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
