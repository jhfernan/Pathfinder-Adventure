<template>
	<section>
		<v-app-bar app clipped-right color="dark" dark fixed>
			<v-toolbar-title v-text="title" />
			<v-spacer />
			<v-app-bar-nav-icon @click.stop="drawer = !drawer" />
		</v-app-bar>
		<v-navigation-drawer
			app
			clipped
			fixed
			right
			v-model="drawer">
			<v-list>
				<v-list-item
					v-for="(item, i) in items"
					:key="i"
					:to="item.to"
					router
					exact
				>
					<v-list-item-action>
						<v-icon>{{ item.icon }}</v-icon>
					</v-list-item-action>
					<v-list-item-content>
						<v-list-item-title v-text="item.title" />
					</v-list-item-content>
				</v-list-item>
			</v-list>
		</v-navigation-drawer>
	</section>
</template>

<script>
export default {
	data () {
		return {
			drawer: false,
			items: [
				{
					icon: 'mdi-apps',
					title: 'Home',
					to: '/'
				},
				{
					icon: 'mdi-apps',
					title: 'Character Tool',
					to: '/character_tool'
				},
			],
			title: 'Pathfinder Adventures'
		}
	}
}
</script>
