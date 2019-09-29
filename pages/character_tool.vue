<template>
	<v-container>
		<h1>Character Tool</h1>
		<v-row>
			<v-col xs="12" md="5">
				<v-card :class="`elevation-${elevation} mb-5`">
					<v-card-text>
						<basic-info :character="character" />
					</v-card-text>
				</v-card>
				<v-card :class="`elevation-${elevation}`">
					<v-card-text>
						<ability-score :character="character" />
					</v-card-text>
				</v-card>
			</v-col>

			<v-col xs="12" md="7">
				<v-card :class="`elevation-${elevation}`">
					<v-tabs vertical>
						<v-tab>
							<!-- <v-icon left>mdi-account</v-icon> -->
							HP and Status Tracker
						</v-tab>
						<v-tab>
							<!-- <v-icon left>mdi-lock</v-icon> -->
							Weapons and Attacks
						</v-tab>
						<v-tab>
							<!-- <v-icon left>mdi-lock</v-icon> -->
							Skill Checks
						</v-tab>

						<v-tab-item>
							<v-card flat>
								<v-card-text>
									Not done yet...
								</v-card-text>
							</v-card>
						</v-tab-item>

						<v-tab-item>
							<v-card flat>
								<v-card-text>
									Not done yet...
								</v-card-text>
							</v-card>
						</v-tab-item>

						<v-tab-item>
							<v-card flat>
								<v-card-text>
									<skill-checker />
								</v-card-text>
							</v-card>
						</v-tab-item>
					</v-tabs>
				</v-card>
			</v-col>
		</v-row>
	</v-container>
</template>

<script>
import AbilityScore from '~/components/character/AbilityScore'
import BasicInfo from '~/components/character/BasicInfo'
import SkillChecker from '~/components/character/SkillChecker'

export default {
	asyncData ({ app, error }) {
		return app.$axios.$get('/character.json')
		.then(res => {
			return { character: res }
		})
		.catch(err => { error({ statusCode: '404', message: 'Could not find Character info' }) })
	},
	components: { AbilityScore, BasicInfo, SkillChecker },
	data () {
		return {
			elevation: 12
		}
	}
}
</script>
