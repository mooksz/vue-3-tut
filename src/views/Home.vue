<template>
	<div class="home">
		<UserProfile />
	</div>
</template>

<script>
	import UserProfile from "@/components/UserProfile";

	export default {
		name: "Home",
		components: {
			UserProfile,
		},
	};
</script>

<style scoped lang="scss">
	.home {
		width: 100%;
	}
</style>
