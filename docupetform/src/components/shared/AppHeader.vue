<template>
	<header class="el-header">
		<div class="navbar-wrapper">
			<div class="logo-container">
				<el-image
					class="logo"
					:src="require('@/assets/docupet-logo.png')"
					fit="contain"
					alt="DocuPet"
				/>
				<nav class="navbar-menu menu">
					<a class="menu-item" href="/">Help</a>
					<a class="menu-item--blue" href="/">Save and Finish Later</a>
				</nav>
			</div>
		</div>
	</header>
</template>
<script>
export default {
	name: "AppFooter",
};
</script>
<style></style>
