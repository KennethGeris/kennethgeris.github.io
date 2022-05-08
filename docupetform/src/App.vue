<template>
	<div class="common-layout">
		<AppHeader />
		<el-container direction="vertical">
			<el-main>
				<ContactForm />
				<AppFooter />
			</el-main>
		</el-container>
	</div>
</template>

<script>
import AppHeader from "./components/shared/AppHeader.vue";
import AppFooter from "./components/shared/AppFooter.vue";
import ContactForm from "./components/ContactForm.vue";

export default {
	name: "App",
	components: {
		AppHeader,
		AppFooter,
		ContactForm,
	},
};
</script>

<style>
#app {
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
}
</style>
<style src="./styles/main.scss" lang="scss" />
