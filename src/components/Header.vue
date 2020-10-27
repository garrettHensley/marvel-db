<template>
	<a href="#">
		<b-jumbotron class="py-3">
			<b-img :src="require('../assets/logo.png')" fluid />
			<h1>Database</h1>
		</b-jumbotron>
	</a>
</template>

<script>
export default {};
</script>

<style scoped>
.jumbotron {
	color: white;
	background: #ee161f;
}
.jumbotron img {
	max-width: 35em;
}
.jumbotron h1 {
	font-size: 3em;
	margin-bottom: 0;
}
</style>
