<template>
	<div class="slider">
		<div class="container">
			<div ref="swiper" class="swiper">
				<div class="swiper-wrapper">
					<div
						v-for="(slide, index) in slides"
						:key="index"
						class="swiper-slide"
					>
						<img :src="slide" alt="" />
					</div>
				</div>

				<div class="swiper-pagination"></div>
				<div class="swiper-button-prev"></div>
				<div class="swiper-button-next"></div>

				<div class="swiper-scrollbar"></div>
			</div>
		</div>
	</div>
</template>

<script>
import Swiper, { Navigation, Pagination } from "swiper";
import "swiper/css";
import "swiper/css/navigation";
import "swiper/css/pagination";

export default {
	props: ["slides"],
	mounted() {
		new Swiper(this.$refs.swiper, {
			modules: [Navigation, Pagination],
			loop: true,
			observeSlideChildren: true,
			observeParents: true,
			observer: true,
			pagination: {
				el: ".swiper-pagination",
			},

			navigation: {
				nextEl: ".swiper-button-next",
				prevEl: ".swiper-button-prev",
			},

			scrollbar: {
				el: ".swiper-scrollbar",
			},

			breakpoints: {
				320: {
					slidesPerView: 1,
				},
				768: {
					slidesPerView: 2,
					spaceBetween: 30,
				},
				1440: {
					slidesPerView: 3,
					spaceBetween: 30,
				},
			},
		});
	},
};
</script>

<style lang="scss">
.slider {
	margin-top: 16px;
	.swiper {
		height: 330px;
		&-slide {
			width: 442px;
			height: 294px;
			img {
				width: 100%;
				height: 100%;
				object-fit: cover;
			}
		}
		&-pagination {
			bottom: 0;
			&-bullet {
				width: 12px;
				height: 12px;
			}
			&-bullet-active {
				background-color: #5775a9;
			}
		}
		&-button-prev,
		&-button-next {
			background: rgba(0, 0, 0, 0.5);
			width: 48px;
			height: 48px;
			border-radius: 50%;
			&::after {
				font-size: 18px;
				font-weight: 600;
				color: white;
			}
		}
	}
}
</style>
