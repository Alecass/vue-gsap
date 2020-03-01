<template>
	<svg viewBox="0 0 1920 1080">
		<transition-group
			@before-enter="beforeEnter"
			@enter="enter"
			@leave="leave"
			:css="false"
		>
			<span v-for="circle in circles" :key="circle.id">
				<circle v-if="isVisible" :cx="circle.x" :cy="y" :r="r" />
			</span>
		</transition-group>
	</svg>
</template>

<script>
import gsap from 'gsap'

export default {
	name: 'HelloWorld',
	data() {
		return {
			isVisible: false,
			r: 50,
			y: 1080 + 50,
			circles: [
				{
					id: 0,
					x: 1920 / 3,
				},
				{ id: 1, x: 1920 / 2 },
				{ id: 2, x: 1920 },
			],
		}
	},
	mounted() {
		console.clear()
		console.log('♦ MOUNTED')

		window.addEventListener('keydown', e => {
			console.log('♦ KEYDOWN', e.code)

			if (e.keyCode === 32) {
				this.isVisible = true
			}
		})

		window.addEventListener('keyup', e => {
			console.log('♦ KEYUP', e.code)

			if (e.keyCode === 32) {
				this.isVisible = false
			}
		})
	},
	methods: {
		beforeEnter: el => {
			console.log('♦ BEFOREENTER')

			el.style.opacity = 1
		},
		enter: (el, done) => {
			console.log('♦ ENTERING...')

			let tween = gsap.to(el, {
				opacity: 0,
				ease: 'sine.In',
				duration: 2,

				y: -(1080 / 2),
				onComplete: () => {
					console.log('♦ DONE')
					done()
				},
			})
		},
		leave: (el, done) => {
			console.log('♦ LEAVING...')

			el.style.opacity = 0

			console.log('♦ DONE')
			done()
		},
	},
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped></style>
