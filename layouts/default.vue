<template>
	<v-app>
		<navigation />
		<v-content>
			<nuxt />
		</v-content>
	</v-app>
</template>

<script>
import Navigation from '~/components/Navigation.vue'

export default {
	components: { Navigation },
	data () {
		return {
			drawer: false,
			items: [
				{
					icon: 'mdi-apps',
					title: 'Welcome',
					to: '/'
				},
				{
					icon: 'mdi-chart-bubble',
					title: 'Inspire',
					to: '/inspire'
				}
			],
			miniVariant: false,
			title: 'Pathfinder Adventures'
		}
	}
}
</script>
