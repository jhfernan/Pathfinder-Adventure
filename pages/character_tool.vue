<template>
	<v-container>
		<h1>Character Tool</h1>
		<v-layout>
			<v-flex xs12 md6 lg4>
				<basic-info />
			</v-flex>
		</v-layout>
	</v-container>
</template>

<script>
import BasicInfo from '~/components/character/BasicInfo'

export default {
	asyncData ({ app, error }) {
		return app.$axios.$get('/character.json')
		.then(res => {
			return { character: res }
		})
		.catch(err => { error({ statusCode: '404', message: 'Could not find Character info' }) })
	},
	components: { BasicInfo }
}
</script>
