<template>
	<v-simple-table dense>
		<template v-slot:default>
			<thead>
				<tr>
					<th class="text-center">Skill</th>
					<th class="text-center">Total</th>
					<th class="text-center">Rank</th>
					<th class="text-center">Ability</th>
					<th class="text-center">Trained</th>
					<th class="text-center">Race</th>
					<th class="text-center">Misc</th>
				</tr>
			</thead>
			<tbody class="text-center">
				<tr v-for="(skill, key, i) in skills" :key="i">
					<th class="black text-capitalize white--text">
						{{ key }}
						{{ skill.acCheck ? '*' : '' }} <span class="text-uppercase ml-2">({{ skill.ability }})</span>
					</th>
					<td>{{ total(skill)}} </td>
					<td>{{ skill.ranks != 0 ? skill.ranks : '' }}</td>
					<td>{{ skill.abilityModifier != 0 ? skill.abilityModifier : '' }}</td>
					<td :class="skill.ranks == 0 ? 'red--text' : 'green--text'">
						{{ skill.trained ? skill.trained : '' }}
					</td>
					<td></td>
					<td></td>
				</tr>
			</tbody>
		</template>
	</v-simple-table>
</template>

<script>
import races from '~/components/helpers/races'
import skills from '~/components/helpers/skills'

export default {
	computed: {
		skills () {
			let res = {}
			for (var item of Object.keys(this.allSkills)) {
				res[item] = this.allSkills[item]
				res[item].ranks = this.character.skillRanks[item]
				res[item].abilityModifier = Math.floor(
					(this.character.stats[res[item].ability]
						+ (this.race.ability[res[item].ability] ? this.race.ability[res[item].ability] : 0)
					) / 2) - 5
				res[item].trained = this.race.skillsTrained[item] ? 3 : 0
			}
			return res
		}
	},
	data () {
		return {
			race: races[this.character.race],
			allSkills: skills
		}
	},
	methods: {
		total (skill) {
			let total = 0
			total += skill.ranks ? skill.ranks : 0
			total += skill.abilityModifier ? skill.abilityModifier : 0
			total += skill.trained && skill.ranks > 0 ? skill.trained : 0
			return total
		}
	},
	props: {
		character: {
			type: Object,
			default: function () {
				return {
					stats: {
						str: 8,
						dex: 16,
						con: 10,
						int: 12,
						wis: 12,
						cha: 18
					},
					skillRanks: {
						acrobatics: 1,
						appraise: 0,
						bluff: 0,
						climb: 4,
						craft: 1,
						diplomacy: 4,
						disableDevice: 0,
						disguise: 1,
						escapeArtist: 1,
						fly: 0,
						handleAnimal: 1,
						heal: 0,
						intimidate: 0,
						knArcana: 1,
						knDungeoneering: 1,
						knEngineering: 0,
						knGeography: 0,
						knHistory: 0,
						knLocal: 1,
						knNature: 1,
						knNobility: 1,
						knPlanes: 0,
						knReligion: 1,
						linguistics: 0,
						perception: 1,
						perform: 4,
						profession: 0,
						ride: 0,
						senseMotive: 0,
						sleightOfHand: 1,
						spellcraft: 1,
						stealth: 1,
						survival: 0,
						swim: 0,
						useMagicDevice: 1
					},
					race: 'catfolk',
				}
			}
		},
		// enhanceStats: {
		// 	type: Object,
		// 	default: function () {
		// 		return {}
		// 	}
		// },
		// miscellaneousStats: {
		// 	type: Object,
		// 	default: function () {
		// 		return {}
		// 	}
		// },
	}
}
</script>
