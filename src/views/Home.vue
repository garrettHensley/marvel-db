<template>
	<div>
		<Header />
		<Main />
	</div>
</template>

<script>
import Main from "@/components/Main.vue";
import Header from "@/components/Header.vue";

export default {
	components: {
		Main,
		Header,
	},
};
</script>
