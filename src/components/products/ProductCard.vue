<template>
	<div class="product">
		<div class="product__body">
			<div class="product__img">
				<img :src="product.thumbnail" alt="" />
				<div
					class="product__status"
					:style="{ 'background-color': getStatus(product.id)?.color }"
				>
					{{ getStatus(product.id)?.text }}
				</div>
			</div>
			<!-- :style="{ 'background-color': status.color }" -->
			<div class="product__content">
				<div class="product__content-item">
					<p class="product__content-item--value">
						<span>Brand: </span>{{ product.brand }}
					</p>
				</div>
				<div class="product__content-item">
					<p class="product__content-item--value">
						<span>Category: </span>{{ product.category }}
					</p>
				</div>
				<div class="product__content-item">
					<p class="product__content-item--value description">
						<span>Description: </span>{{ product.description }}
					</p>
				</div>
				<div class="product__content-item">
					<p class="product__content-item--value">
						<span>In stock: </span>{{ stock }}
					</p>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	props: ["product"],
	data() {
		return {
			time: (Math.floor(Math.random() * 4) + 1) * 1000,
			stock: this.product.stock,
			interval: null,
			statusMap: {
				1: {
					text: "top",
					color: "green",
				},
				2: {
					text: "sale",
					color: "orange",
				},
				3: {
					text: "popular",
					color: "purple",
				},
			},
		};
	},
	watch: {
		stock(val) {
			if (val === 0) {
				clearInterval(this.interval);
			}
		},
	},
	methods: {
		getStatus(id) {
			return this.statusMap[id];
		},
	},
	mounted() {
		this.interval = setInterval(() => {
			this.stock = this.stock - 1;
		}, this.time);
	},
};
</script>

<style lang="scss" scoped>
.product {
	padding: 9px;
	border: 1px solid #d9d9d9;
	&__img {
		margin-bottom: 9px;
		position: relative;
		img {
			height: 206px;
			width: 100%;
			object-fit: cover;
		}
	}
	&__status {
		position: absolute;
		top: 10px;
		left: 10px;
		padding: 4px 16px;
		border-radius: 20px;
		color: white;
	}
	&__content {
		&-item {
			display: flex;
			align-items: center;
			margin-bottom: 8px;
			&:last-child {
				margin-bottom: 0;
			}
			p {
				font-size: 16px;
				font-weight: 400;
				color: #111111;
				span {
					font-weight: 600;
				}
			}
			.description {
				display: -webkit-box;
				-webkit-line-clamp: 2;
				-webkit-box-orient: vertical;
				overflow: hidden;
				text-overflow: ellipsis;
			}
		}
	}
}
</style>
