<template>
	<div>
		<div>
			<span class="headline mr-1">{{ character.name }}</span>
			(<em class="subtitle-1 text-capitalize">{{ character.race }} {{ character.class }}</em>)
			<v-icon class="pb-2" :color="character.gender ? 'blue' : 'pink'">
				mdi-gender-{{ character.gender ? 'male' : 'female' }}
			</v-icon>
		</div>
		<div class="subtitle-2">{{ character.player }}</div>
		<div v-if="character.background
			&& character.background.affluence
			&& character.background.occupation
			&& character.background.birthPlace
			&& character.background.parents
			&& diety && languages">
			<span><strong>{{ character.name }}</strong> grew up <strong>{{ character.background.affluence }}</strong>. </span>
			<span>{{ character.gender ? 'He' : 'She' }} was born in </span>
			<span><strong>{{ character.background.birthPlace }}</strong> and grew up </span>
			<strong>
				{{
					character.background.parents == 'two'
						? 'with two wonderful parents'
						: character.background.parents == 'one' && character.background.parent
							? 'with a loving father'
							: character.background.parents == 'one' && !character.background.parent
								? 'with a loving mother'
								: 'alone as a street urchin'
				}}
			</strong>
			<span>. {{ character.gender ? 'He' : 'She' }} worships </span>
			<span v-if="diety.gods">
				the {{ diety.gender }} <strong>{{ diety.name }}</strong>, the {{ diety.gender }} of {{ diety.of }}.
			</span>
			<span v-else>no god or virtue and prefers to believe only in oneself.</span>
			<span> {{ character.gender ? 'He' : 'She' }} speaks <strong>{{ languages }}</strong>.</span>
		</div>
		<div v-else>Background not completed yet.</div>
	</div>
</template>

<script>
export default {
	computed: {
		diety () {
			if (this.character.background && this.character.background.diety)
				var res = {
					name: this.character.background.diety,
					gender: 'god',
					gods: true
				}
				switch (this.character.background.diety) {
					case 'Cayden Cailean':
						res.of = 'Ale/Freedom'
						break
					default:
						res = { gods: false }
			}
			return res
		},
		languages () {
			var res = 'only common tongue'
			if (this.character.background && this.character.background.languages) {
				if (this.character.background.languages.length == 1) {
					res = `only ${this.character.background.languages[0]}`
				} else {
					let response = ''
					for (var language in this.character.background.languages) {
						response += this.character.background.languages.length - 1 == language
							? 'and '
							: ''
						response += this.character.background.languages[language]
						response += this.character.background.languages.length - 1 != language
							? ', '
							: ''
					}
					res = response
				}
			}
			return res
		}
	},
	props: {
		character: {
			type: Object,
			default: function () {
				return {
					name: 'Name',
					race: 'race',
					class: 'class',
					gender: true,
					player: 'Player Name',
					background: {
						affluence: 'poor',
						birthPlace: 'Magnamar',
						diety: 'Cayden Cailean',
						languages: [
							'common',
						],
						occupation: 'Dancer',
						parents: 'one',
						parent: false,
					},
				}
			}
		}
	}
}
</script>
