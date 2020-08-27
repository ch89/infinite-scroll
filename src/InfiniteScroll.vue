<template>
	<!-- @scroll="scroll" -->
	<div class="infinite-scroll" :style="{ height }">
		<slot></slot>
	</div>
</template>

<script>
	export default {
		props: {
			pagination: {
				required: true
			},
			distance: {
				default: 1
			},
			height: {
				default: "500px"
			}
		},
		watch: {
			pagination() {
				if(this.pagination.current_page < this.pagination.last_page) {
					this.$el.addEventListener("scroll", this.scroll)
				}
			}
		},
		methods: {
			scroll(e) {
				if(e.target.scrollTop / (e.target.scrollHeight - e.target.clientHeight) >= this.distance) {
					e.target.removeEventListener("scroll", this.scroll)

					this.$emit("load")
				}	
			}
		}
	}
</script>

<style scoped>
	.infinite-scroll {
		overflow: auto;
		scroll-behavior: smooth;
	}
</style>