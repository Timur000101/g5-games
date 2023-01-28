<template>
	<main class="main-page">
		<Header></Header>
		<Slider :slides="slides"></Slider>
		<ProductList></ProductList>
	</main>
</template>

<script>
import axios from "axios";
import Header from "@/components/Header.vue";
import Slider from "@/components/Slider.vue";
import ProductList from "@/components/products/ProductList.vue";
import { setCookie, getCookie } from "@/utils/cookies";
export default {
	components: {
		Header,
		Slider,
		ProductList,
	},
	data() {
		return {
			slides: [],
		};
	},
	watch: {
		slides: {
			handler: function (val, old) {
				if (val.length <= 10 && getCookie("slider-images") === undefined) {
					this.getImage();
					if (val.length === 10) {
						setCookie("slider-images", JSON.stringify(this.slides), {
							secure: true,
							"max-age": 300,
						});
					}
				}
			},
			deep: true,
		},
	},
	created() {
		if (getCookie("slider-images") === undefined) {
			this.getImage();
		} else {
			this.slides = JSON.parse(getCookie("slider-images"));
		}
	},
	methods: {
		getImage() {
			axios.get("https://random.dog/woof.json").then((res) => {
				if (res.status === 200) {
					if (res.data.url.substr(res.data.url.length - 3) !== "mp4") {
						this.slides = [...this.slides, res.data.url];
					} else {
						this.getImage();
					}
				}
			});
		},
	},
};
</script>
