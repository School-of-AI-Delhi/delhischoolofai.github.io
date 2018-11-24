<template>
	<v-toolbar color="primary" dark>
		<v-toolbar-side-icon class="hidden-md-and-up" @click.stop="drawer = !drawer"></v-toolbar-side-icon>
		<v-navigation-drawer v-model="drawer" absolute temporary style="max-height: 100vh; height: 100vh;">
			<v-list>
				<v-list-tile v-for="(navItem, index) in navItems" :key="index" :to="navItem.route">
					<v-list-tile-action>
						<v-icon>{{ navItem.icon }}</v-icon>
					</v-list-tile-action>
					<v-list-tile-content>
						<v-list-tile-title>{{ navItem.name }}</v-list-tile-title>
					</v-list-tile-content>
				</v-list-tile>
			</v-list>
		</v-navigation-drawer>
		<v-toolbar-title>
			<router-link to="/" class="app-name" tag="span">Delhi School of AI</router-link>
		</v-toolbar-title>
		<v-spacer></v-spacer>
		<v-toolbar-items class="hidden-sm-and-down">
			<v-btn flat v-for="(navItem, index) in navItems" :key="index" :to="navItem.route">{{ navItem.name }}</v-btn>
		</v-toolbar-items>
	</v-toolbar>
</template>

<script>
export default {
  name: 'NavBar',
  data() {
	  return {
		  navItems: [{name: 'Events', route: '/events', icon: ''},
					{name: 'About Us', route: '/about', icon: ''},
					{name: 'Contact', route: '/contact-us', icon: ''}],
		  drawer: false
	  }
  }
}
</script>

<style scoped>
	.app-name {
		cursor: pointer;
	}
</style>
