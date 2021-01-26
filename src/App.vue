<template>
	<div id="app">
		<h1 class="text-center bg-gray-100 py-4 font-bold capitalize ">Made with vue 3, tailwind css 2</h1>
		<Calculator />
	</div>
</template>

<script>
	import Calculator from "./components/Calculator.vue";
export default {
  components: {
    Calculator
  }
};
</script>

<style lang="scss">
</style>