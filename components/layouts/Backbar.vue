<template>
	<section>
		<v-app-bar app clipped-right fixed>
			<v-toolbar-title v-text="title" />
			<v-spacer />
			<v-app-bar-nav-icon @click.stop="drawer = !drawer" />
			<v-btn @click.stop="miniVariant = !miniVariant" icon>
				<v-icon>mdi-{{ `chevron-${miniVariant ? 'right' : 'left'}` }}</v-icon>
			</v-btn>
		</v-app-bar>
		<v-navigation-drawer
			app
			clipped
			fixed
			:mini-variant="miniVariant"
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
					title: 'Welcome',
					to: '/'
				},
			],
			miniVariant: false,
			title: 'Backend'
		}
	}
}
</script>
