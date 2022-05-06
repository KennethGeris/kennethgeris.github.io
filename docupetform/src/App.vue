<template>
	<AppHeader />
	<ContactForm />
	<AppFooter />
</template>

<script>
import AppHeader from "./components/shared/AppHeader";
import AppFooter from "./components/shared/AppFooter";
import ContactForm from "./components/ContactForm";

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
	text-align: center;
	color: #2c3e50;
	margin-top: 60px;
}
</style>
<style src="./styles/main.scss" lang="scss" />
