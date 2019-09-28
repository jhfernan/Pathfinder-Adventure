<template>
	<v-container>
		<h1>Character Tool</h1>
		<v-row>
			<v-col xs="12" md="4">
				<basic-info :character="character" />
				<div class="py-3"></div>
				<ability-score />
			</v-col>
			<v-col xs="12" md="8">
				<basic-info :character="character" />
			</v-col>
		</v-row>
	</v-container>
</template>

<script>
import AbilityScore from '~/components/character/AbilityScore'
import BasicInfo from '~/components/character/BasicInfo'

export default {
	asyncData ({ app, error }) {
		return app.$axios.$get('/character.json')
		.then(res => {
			return { character: res }
		})
		.catch(err => { error({ statusCode: '404', message: 'Could not find Character info' }) })
	},
	components: { AbilityScore, BasicInfo },
}
</script>
