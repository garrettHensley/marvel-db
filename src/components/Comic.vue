<template>
	<b-col cols="4" @click="show">
		<!-- These comics should just be converted into the bootstrap card class? -->
		<div>
			<img :src="image" class="img-fluid" />
			<p class="lead">{{ title }}</p>
		</div>
		<!-- When Comic is clicked, fullview is turned on or off // I want this to open up to the side of the comic -->
		<b-modal ref="comicModal" size="lg" centered>
			<h1>{{ title }}</h1>
			<p class="font-italic">{{ description }}</p>
			Created by:
			<ul class="text-left">
				<span v-for="creator in creators" :key="creator.id">
					<li
						v-if="
							creator.role == 'writer' ||
								creator.role == 'colorist' ||
								creator.role == 'inker'
						"
					>
						{{ creator.name }}
						({{ creator.role }})
					</li>
				</span>
			</ul>
			<p>Features:</p>
			<ul>
				<li>
					<span v-for="character in characters" :key="character.id"
						>{{ character.name }},
					</span>
				</li>
			</ul>
		</b-modal>
	</b-col>
</template>

<script>
export default {
	props: {
		title: String,
		image: String,
		description: String,
		date: String,
		creators: Array,
		characters: Array,
	},

	methods: {
		show() {
			this.$refs["comicModal"].show();
			console.log("show modal");
		},
		hide() {
			this.$refs["comicModal"].hide();
		},
	},
};
</script>

<style>
.modal-content {
	color: white;
	background: #1f2d3d !important;
	-webkit-box-shadow: 0px 0px 10px 3px rgba(0, 0, 0, 0.75);
	-moz-box-shadow: 0px 0px 10px 3px rgba(0, 0, 0, 0.75);
	box-shadow: 0px 0px 10px 3px rgba(0, 0, 0, 0.575);
}
.modal-header,
.modal-footer {
	border-bottom: none !important;
	border-top: none !important;
}

li {
	list-style: none;
}
.close {
	color: red !important;
	text-shadow: none !important;
	opacity: 1 !important;
}
</style>
