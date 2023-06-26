<template>
	<div class="plan-map">
		<svg viewBox="0 0 1477 1140">
			<image
					class="parking-list__svg"
					ref="parking-list__svg"
					:width="parkings.width"
					:heigth="parkings.height"
					:href="image"
			></image>
			<SvgMap
					id="close"
					v-for="(item, index) in coordinates"
					:key="index"
					:item="item"
					@mousemove.native="tooltipOPen"
			/>
		</svg>
		<div class="tooltip" v-if="toolTip">
			<div class="tooltip__wrapper">
				<div class="tooltip__info">
					<div class="tooltip__description">
						<p>Описание</p>
					</div>
				</div>
			</div>
		</div>
	</div>

</template>

<script>
import coordinates from '/assets/data/map.json'

export default {
	name: "Plan",
	components: {},
	computed: {},
	props: {},
	data() {
		return {
			parkings: {
				width: 1477,
				height: 1140,
			},
			image: require('/static/images/mina.jpg'),
			coordinates,
			toolTip: false,
		}
	},
	async mounted() {
		document.addEventListener('mouseover', (e) => {
			if (!e.target.closest('#close')) {
				this.toolTip = false
			}
		})
	},
	methods: {
		tooltipOPen(e) {
			let toolTip = document.querySelectorAll('.tooltip');
			toolTip.forEach(function (el) {
				let x = e.clientX,
						y = e.clientY;
				el.style.top = (y + 20) + 'px';
				el.style.left = (x + 20) + 'px';
			})
			this.toolTip = true
		},
		showInfo() {
			this.toolTip = true
			// document.body.style.overflow = 'hidden';
		},
		closePopup() {
			// document.body.style.overflow = 'auto';
			this.toolTip = false
		},
	}
}
</script>

<style lang="scss" scoped>
.tooltip {
	position: absolute;
	cursor: pointer;
	&__info{
		width: 100px;
		height: 50px;
		background-color: $white;
		border-radius: 10px;
		display: flex;
		justify-content: center;
		align-items: center;
	}
}

.hovering.marker {
	transition: 0.3s;
	opacity: 1;
}
</style>
