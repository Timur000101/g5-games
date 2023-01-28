<template>
	<div class="products">
		<div class="container">
			<div class="products__inner">
				<Product
					v-for="product in products"
					:key="product.id"
					:product="product"
				></Product>
			</div>
		</div>
	</div>
</template>

<script>
import axios from "axios";
import Product from "./ProductCard.vue";
export default {
	components: {
		Product,
	},
	data() {
		return {
			products: [],
			visible: false,
		};
	},
	created() {
		if (!localStorage.products) {
			axios.get("https://dummyjson.com/products?limit=100").then((res) => {
				this.products = res.data.products;
				localStorage.setItem("products", JSON.stringify(res.data.products));
			});
		} else {
			this.products = JSON.parse(localStorage.products);
		}
	},
};
</script>

<style lang="scss" scoped>
@import "@/assets/styles/mixins.scss";
.products {
	margin: 26px 0;
	&__inner {
		display: grid;
		grid-template-columns: repeat(auto-fill, minmax(252px, 1fr));
		grid-gap: 16px 30px;
	}
}
</style>
