<template>
	<div class="paw-progress">
		<span
			v-for="index in max"
			:key="index"
			v-bind:class="{ active: index <= active }"
		>
			<el-image
				:src="require('@/assets/paws.svg')"
				fit="contain"
				alt="paw progress"
			/>
		</span>
	</div>
</template>
<script>
export default {
	name: "PawProgress",
	props: {
		max: Number,
		active: Number,
	},
};
</script>
<style></style>
