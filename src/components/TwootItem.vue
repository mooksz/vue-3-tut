<template>
	<li class="twoot-item" @click="favoriteTwoot(twoot.id)">
		<div class="twoot-item__user">@{{ username }}</div>

		<div class="twoot-item__content">
			{{ twoot.content }}
		</div>
	</li>
</template>

<script>
	export default {
		name: "TwootItem",
		props: {
			username: {
				type: String,
				required: true,
			},
			twoot: {
				type: Object,
				required: true,
			},
		},
		methods: {
			favoriteTwoot(id) {
				this.$emit("favorite", id);
			},
		},
	};
</script>

<style lang="scss" scoped>
	.twoot-item {
		padding: 2rem;
		background-color: white;
		border-radius: 0.5rem;
		border: 1px solid #dfe3e8;
		cursor: pointer;
		transition: all 0.2s ease-in-out;
		margin: 0 0 0.5rem 0;

		&:hover {
			transform: scale(1.05);
		}

		&__content {
			margin: 0.5rem 0 0 0;
		}

		&__user {
			font-weight: bold;
			font-size: 1.4rem;
		}
	}
</style>
