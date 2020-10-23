<template>
	<b-container id="main" fluid="lg" class="pb-3">
		<Input @input="handleInput" />
		<b-list-group
			v-if="currentView == 'listView'"
			class=" px-4 py-3 rounded-bottom"
		>
			<!-- Create Character components for every character in results array, pass in data to props -->
			<div v-for="character in info" :key="character.id">
				<b-row>
					<b-col>
						<b-list-group-item
							:style="
								`background: url(${character.thumbnail.path}.jpg); background-size: cover; background-repeat: no-repeat; background-position-y: center`
							"
						>
							<div class="list-name">
								<span>{{ character.name }}</span>
							</div>
						</b-list-group-item>
					</b-col>

					<div class="d-flex align-items-center">
						<b-button
							id="profile-button"
							@click="
								(currentView = 'profileView'),
									(selectedCharId = character.id),
									(selectedCharName = character.name),
									(selectedCharPic =
										character.thumbnail.path +
										'.' +
										character.thumbnail.extension)
							"
							size="lg"
							>Profile</b-button
						>
					</div>
				</b-row>
			</div>
		</b-list-group>
		<Profile
			v-if="currentView == 'profileView'"
			:characterId="selectedCharId"
			:Name="selectedCharName"
			:Pic="selectedCharPic"
		/>
	</b-container>
</template>

<script>
import axios from "axios";
import _ from "lodash";
import Profile from "@/components/Profile.vue";
import Input from "@/components/Input.vue";

export default {
	name: "Home",
	components: {
		Input,
		Profile,
	},
	data() {
		return {
			info: null,
			publicKey: "4327819a4e9ae453434bb3d2dcc52456",
			time: 1564731162583,
			currentView: "listView", //default display- charList. can switch to profile view
			selectedCharId: "",
			selectedCharName: "",
			selectedCharPic: "",
		};
	},
	props: {
		searchName: String,
	},
	mounted() {
		this.getUrl(); // initial api request, will be updated by watcher function on searchName
	},
	methods: {
		getUrl() {
			if (this.Search) {
				axios
					.get(
						`https://gateway.marvel.com/v1/public/characters?&nameStartsWith=${
							this.Search
						}&ts=1&apikey=${
							this.publicKey
						}&hash=${"4dfd3313409d3a26b9513377ea1c2698".toLowerCase()}`
					)
					.then((response) => (this.info = response.data.data.results));
			} else {
				axios
					.get(
						`https://gateway.marvel.com/v1/public/characters?&ts=1&apikey=${
							this.publicKey
						}&hash=${"4dfd3313409d3a26b9513377ea1c2698".toLowerCase()}` //store this hashcode in a variable later please
					)
					.then((response) => (this.info = response.data.data.results));
			}
		},
		handleInput(value) {
			this.handleSearch(value);
		},
		showDesc() {},
		handleSearch: _.debounce(function(term) {
			if (this.currentView === "listView") {
				// actually remove this keep updating list if user types, and then if currentView isnt charList set it to that
				if (term) {
					axios
						.get(
							`https://gateway.marvel.com/v1/public/characters?&nameStartsWith=${term}&ts=1&apikey=${
								this.publicKey
							}&hash=${"4dfd3313409d3a26b9513377ea1c2698".toLowerCase()}`
						)
						.then((response) => (this.info = response.data.data.results));
				} else {
					axios
						.get(
							`https://gateway.marvel.com/v1/public/characters?&ts=1&apikey=${
								this.publicKey
							}&hash=${"4dfd3313409d3a26b9513377ea1c2698".toLowerCase()}`
						)
						.then((response) => (this.info = response.data.data.results));
				}
			} else {
				this.currentView = "listView";
			}
		}, 800),
	},

	watch: {
		// When searchName is changed update list of characters live

		searchName: function() {},
	},

	computed: {
		//get rid of this function
		Search() {
			return this.searchName;
		},
	},
};
</script>

<style>
.list-group {
	background: #f9fafc;
}

.list-group-item {
	border-color: #30303081 !important;
	border-left: none !important;
	border-right: none !important;
	padding: 0 !important;
	height: 4em;

	-webkit-box-shadow: 0px 0px 10px 3px rgba(0, 0, 0, 0.75);
	-moz-box-shadow: 0px 0px 10px 3px rgba(0, 0, 0, 0.75);
	box-shadow: 0px 0px 10px 3px rgba(0, 0, 0, 0.75);
}

#profile-button {
	background-color: #1fb6ff;
	color: #fcf9f3;
	font-weight: bolder; /* not sure if we want this */

	border: 1px solid #8492a65e;

	-webkit-box-shadow: 10px 10px 16px -10px rgba(0, 0, 0, 0.75);
	-moz-box-shadow: 10px 10px 16px -10px rgba(0, 0, 0, 0.75);
	box-shadow: 10px 10px 16px -10px rgba(0, 0, 0, 0.75);
}

.list-name {
	background: #1f2d3d4b;
	color: white;
	font-weight: bolder;
	text-shadow: rgb(0, 0, 0) 1px 0 0.1em;
	display: flex;
	justify-content: center;
	align-items: center;
	height: 4em;
}
.list-name span {
	text-align: center;
	font-size: 1.5em;
}
</style>
