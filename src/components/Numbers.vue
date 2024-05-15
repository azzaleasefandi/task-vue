<script setup lang="ts">
import { ref } from 'vue'; // Using the ref function to declare reactive variables.

// Removed line of code number 2 in original file. No need to declare numbers as global variable because it is only being used in one private function

let randomNumbers = ref<number[]>([]);
let highlightedDivisors = ref<number[]>([]);
let limit = ref(100);

// Renamed function n with generateNumbers to have a significant name
// Inside for loop initialization, replaced i value 0 with 1 because the requirement was to display number 1 to 100. And the condition should be i less than and equal to limit.

function generateNumbers() 
{
	let numbers = [];
	for(var i = 1; i <= limit.value; i++) { numbers = [...numbers, i]; }

  	randomNumbers.value = numbers.sort(() => Math.random() - 0.5);
}

// Renamed function hov with highlightDivisors to have a significant name

function highlightDivisors(number: number) {
  const divisors: number[] = [];
  for (let i = 1; i <= number; i++) {
    if (number % i === 0) {
      divisors.push(i);
	  console.log('divisor', divisors)
    }
  }
  highlightedDivisors.value = divisors;
}

function reset() 
{
  highlightedDivisors.value = [];
}

generateNumbers(); // Call the function to generate numbers when component mounts
</script>

// Added minimum and maximum value in input tag to display only number from 1 to 100.
// Added on change function in input tag so that it would display new input number. 

<template>
	<div>
		<input type="number" v-model="limit" min="1" max="100" @change="generateNumbers" /><br /><br />
		<div class="number"
			:id="'number-'+number"
			v-for="number in randomNumbers" 
			:key="number"
			@mouseover="highlightDivisors(number)" 
			@mouseleave="reset"
			:class="{ 'active': highlightedDivisors.includes(number) }"
		>
			{{ number }}
		</div>
	</div>
</template>

<style>
.number {
	display: inline-block;
	padding: 5px;
	background-color: lightgrey;
	margin: 5px;
}

.active {
	background-color: red;
}
</style>
