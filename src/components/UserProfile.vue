<template>
	<div class="user-profile">
		<div class="user-profile__user-panel">
			<h1 class="user-profile__username">@{{ user.username }}</h1>

			<div class="user-profile__admin-badge" v-if="user.isAdmin">admin</div>
			<div v-else class="user-profile__admin-badge">user</div>

			<div class="user-profile__follow-count">
				<strong>Followers: </strong> {{ followers }}
			</div>

			<form class="user-profile__create-twoot" @submit.prevent="onSubmit">
				<label for="newTwoot"><strong>New Twoot</strong></label>
				<textarea
					name="newTwoot"
					id="newTwoot"
					rows="4"
					v-model="newTwootContent"
				></textarea>

				<!-- <div class="user-profile__twoot-type"> -->
				<label v-if="twootTypes.length" for="newTwootType"
					><strong>Choose Twoot type:</strong></label
				>
				<select
					v-if="twootTypes.length"
					v-model="selectedTwootType"
					name="newTwootType"
					id="newTwootType"
				>
					<option
						v-for="twootType in twootTypes"
						:value="twootType.value"
						:key="twootType.value"
						>{{ twootType.label }}</option
					>
				</select>
				<!-- </div> -->
			</form>
		</div>

		<ul class="user-profile__twoots" v-if="user.twoots.length">
			<TwootItem
				v-for="twoot in user.twoots"
				:key="twoot.id"
				:username="user.username"
				:twoot="twoot"
				@favorite="toggleFavorite"
			/>
		</ul>
	</div>
</template>

<script>
	import TwootItem from "./TwootItem";

	export default {
		name: "UserProfile",
		components: {
			TwootItem,
		},
		data() {
			return {
				newTwootContent: "",
				selectedTwootType: "publish",
				twootTypes: [
					{ value: "draft", label: "Draft" },
					{ value: "publish", label: "Publish" },
				],
				followers: 0,
				user: {
					id: 1,
					username: "mhaklander",
					firstName: "Mikey",
					lastName: "Haklander",
					email: "mike@the-pack.nl",
					isAdmin: true,
					twoots: [
						{
							id: 1,
							content: "Twotter is amazing",
						},
						{
							id: 2,
							content: "Don't forget to subscribe to The Pack - Digital Agency boss",
						},
					],
				},
			};
		},
		watch: {
			followers(newCount, oldCount) {
				if (oldCount < newCount) {
					console.log("🙋‍♂️", `${this.user.username} has gained a follower!`);
				}
			},
		},
		computed: {
			fullName() {
				return `${this.user.firstName} ${this.user.lastName}`;
			},
		},
		methods: {
			followUser() {
				this.followers++;
			},
			toggleFavorite(id) {
				console.log("🙋‍♂️", `Favorited Twoot #${id}`);
			},
		},
		mounted() {
			this.followUser();
		},
	};
</script>

<style scoped lang="scss">
	.user-profile {
		display: grid;
		grid-template-columns: 1fr 3fr;
		width: 100%;
		padding: 5rem 2.5rem;

		&__username {
			margin: 0 0 0.4rem 0;
		}

		&__user-panel {
			display: flex;
			flex-direction: column;
			margin: 0 1.5rem 0 0;
			padding: 1.5rem;
			background-color: white;
			border-radius: 5px;
			border: 1px solid #dfe3e8;
		}

		&__admin-badge {
			background-color: rebeccapurple;
			color: white;
			border-radius: 0.5rem;
			margin: 0 auto 1rem 0;
			padding: 0.2rem 1rem;
			font-weight: bold;
		}

		&__twoots {
			list-style: none;
			padding: 0;
			margin: 0;
		}

		&__create-twoot {
			display: flex;
			flex-direction: column;
			margin: 1.5rem 0 0 0;
			border-top: 1px solid lightgray;
			padding: 1rem 0 0 0;

			label {
				margin: 1rem 0 0.5rem 0;
			}

			textarea {
				resize: vertical;
			}
		}
	}
</style>
