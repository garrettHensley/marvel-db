<template>
	<div id="profile">
		<b-jumbotron
			class="d-flex align-items-center justify-content-around rounded-0"
		>
			<h1 class="display-4">{{ Name }}</h1>

			<img :src="Pic" class="fluid w-25 h-25 rounded" />
		</b-jumbotron>
		<div class="row">
			<!-- I need to format the comics better, and make the titles stand out better with each comic. For now I'm just making every other comic a different bg color -->

			<!-- MAKE ALL OF THIS INSIDE HERE A COMPONENT Comic.vue -->

			<Comic
				v-for="(comic, index) in info"
				:key="comic.id"
				:title="comic.title"
				:image="comic.thumbnail.path + '.' + comic.thumbnail.extension"
				:description="comic.description"
				:creators="comic.creators.items"
				:characters="comic.characters.items"
				class="p-3 text-center"
				:class="[index % 2 === 0 ? 'bg-one' : 'bg-two']"
			/>
		</div>
	</div>
</template>

<script>
import axios from "axios";
import Comic from "@/components/Comic.vue";

export default {
	components: {
		Comic,
	},
	props: {
		characterId: Number,
		Name: String,
		Pic: String,
		description: String, // turn all of this into a big ole object please ;)
	},
	data() {
		return {
			info: null,
			hash: "4dfd3313409d3a26b9513377ea1c2698",
			publicKey: "4327819a4e9ae453434bb3d2dcc52456",
			time: 1,
		};
	},
	mounted() {
		this.getUrl();
	},
	methods: {
		getUrl() {
			axios
				.get(
					`https://gateway.marvel.com/v1/public/characters/${this.characterId}/comics?apikey=4327819a4e9ae453434bb3d2dcc52456&ts=1&hash=4dfd3313409d3a26b9513377ea1c2698`
				)
				.then((response) => (this.info = response.data.data.results));
			console.log(
				`https://gateway.marvel.com/v1/public/characters/${this.characterId}/comics?apikey=4327819a4e9ae453434bb3d2dcc52456&ts=1&hash=4dfd3313409d3a26b9513377ea1c2698`
			);
		},
	},
};
</script>

<style scoped>
#profile {
	background: rgb(39, 52, 68);
	background: linear-gradient(
		45deg,
		rgba(39, 52, 68, 1) 0%,
		rgba(60, 72, 88, 1) 100%
	);
}
.jumbotron {
	background: transparent;
}
h1 {
	background: -webkit-linear-gradient(#ffc82c, #ff7849);
	-webkit-background-clip: text;
	-webkit-text-fill-color: transparent;
}
.row {
	margin-left: 0;
	margin-right: 0;
}
.bg-one,
.bg-two {
	color: white;
}
.bg-one {
	background: #273444;
}
.bg-two {
	background: transparent;
}
</style>
