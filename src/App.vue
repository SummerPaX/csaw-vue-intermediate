<script setup lang="ts">
import { ref } from "vue";
import { v4 as uuidv4 } from "uuid";

const items = ref([
	{
		id: 124,
		name: "Max",
	},
	{
		id: 231,
		name: "Thomas",
	},
	{
		id: 65,
		name: "Julia",
	},
	{
		id: 32,
		name: "Franziska",
	},
]);

function addRandomName() {
	const randomNumber = uuidv4();

	items.value.unshift({
		id: randomNumber,
		name: "Name " + randomNumber,
	});
}

function getRandomInt(max: number) {
	return Math.floor(Math.random() * max);
}

function removeRandomName() {
	items.value.splice(getRandomInt(items.value.length), 1);
}

function randomSort() {
	items.value.sort((a) => getRandomInt(2) - 1);
}
</script>

<template>
	<button @click="addRandomName">Add Name</button>
	<button @click="removeRandomName">Remove Name</button>
	<button @click="randomSort">Random Sort</button>

	<TransitionGroup class="block" name="list" tag="div">
		<p v-for="item in items" :key="item.id">{{ item.name }}</p>
	</TransitionGroup>
</template>

<style scoped>
.list-move, /* apply transition to moving elements */
.list-enter-active,
.list-leave-active {
	transition: all 0.5s ease;
}

.list-enter-from,
.list-leave-to {
	opacity: 0;
	transform: translateX(30px);
}

/* ensure leaving items are taken out of layout flow so that moving
   animations can be calculated correctly. */
.list-leave-active {
	position: absolute;
}
</style>
