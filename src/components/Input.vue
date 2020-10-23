<template>
	<b-input-group size="lg">
		<!-- This input should be moved to Main.vue  -->
		<b-form-input
			type="text"
			v-model="search"
			@input="handleInput"
			class="rounded form-control text-center w-75"
			placeholder="Search for Marvel characters"
		/>
	</b-input-group>
</template>

<script>
export default {
	data() {
		return {
			search: "",
		};
	},
	methods: {
		handleInput() {
			this.$emit("input", this.search);
		},
	},
};
</script>

<style scoped></style>
