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
					<td></td>
					<td></td>
					<td></td>
					<td></td>
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
			return this.allSkills
		}
	},
	data () {
		return {
			race: races[this.character.race],
			allSkills: skills
		}
	},
	methods: {
		// modifier (stat, type) {
		// 	let res = Math.floor(
		// 		(stat + (this.inherentStats[type]
		// 			? this.inherentStats[type]
		// 			: 0)
		// 		) / 2) - 5
		// 	return res
		// },
		// total (stat, type) {
		// 	let res = stat
		// 	res += this.inherentStats[type]
		// 		? this.inherentStats[type]
		// 		: 0
		// 	res += this.enhanceStats[type]
		// 		? this.enhanceStats[type]
		// 		: 0
		// 	res += this.miscellaneousStats[type]
		// 		? this.miscellaneousStats[type]
		// 		: 0
		// 	return res
		// }
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
					skills: {
						acrobatics: true,
						knArcana: true
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
