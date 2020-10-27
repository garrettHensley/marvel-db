<template>
	<div>
		<b-list-group-item @click="showDesc = !showDesc" class="lead">
			{{ name }}
			<b-icon-caret-up-fill v-if="!showDesc && description" />
			<b-icon-caret-down-fill v-if="showDesc && description" />
		</b-list-group-item>
		<b-list-group-item
			v-if="showDesc && description"
			class="bg-dark text-light"
		>
			<b-img width="75" fluid :src="thumbnail" />
			{{ description }}
		</b-list-group-item>
	</div>
</template>

<script>
export default {
	data() {
		return {
			showDesc: false,
		};
	},
	props: {
		name: String,
		description: String,
		comics: Array,
		thumbnail: String,
	},
};
</script>
