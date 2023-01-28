<template>
	<header class="header">
		<div class="container">
			<div class="header__inner">
				<img class="logo" src="@/assets/logo.svg" alt="logo" />
				<button class="btn">Update Products</button>
			</div>
		</div>
	</header>
</template>

<script>
export default {
	data() {
		return {};
	},
};
</script>

<style lang="scss" scoped>
.header {
	width: 100%;
	height: 48px;
	position: sticky;
	top: 0;
	left: 0;
	background-color: #5775a9;
	z-index: 100;
	&__inner {
		display: flex;
		justify-content: space-between;
		align-items: center;
		height: 100%;
		@media (max-width: 768px) {
			visibility: hidden;
		}
	}
}
</style>
