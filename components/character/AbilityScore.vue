<template>
	<v-card :class="`elevation-${elevation}`">
		<v-card-text>
			<v-simple-table>
				<template v-slot:default>
					<thead>
						<tr>
							<th></th>
							<th class="text-center">Total</th>
							<th class="text-center">Modifier</th>
							<th class="text-center">Base</th>
							<th class="text-center">Inherent</th>
							<th class="text-center">Enhance</th>
							<th class="text-center">Misc</th>
						</tr>
					</thead>
					<tbody class="text-center">
						<tr v-for="(stat, key, i) in character.stats" :key="i">
							<th class="black subtitle-1 text-center text-uppercase white--text">
								{{ key }}
							</th>
							<td>{{ total(stat, key) }}</td>
							<td>
								{{ modifier(stat, key) > 0 ? '+' : modifier(stat, key) < 0 ? '-' : '' }}
								{{ modifier(stat, key) }}
							</td>
							<td>{{ stat }}</td>
							<td>{{ inherentStats[key] ? inherentStats[key] : '' }}</td>
							<td>{{ enhanceStats[key] ? enhanceStats[key] : '' }}</td>
							<td>{{ miscellaneousStats[key] ? miscellaneousStats[key] : '' }}</td>
						</tr>
					</tbody>
				</template>
			</v-simple-table>
		</v-card-text>
	</v-card>
</template>

<script>
import util from '~/components/helpers/character'

export default {
	data () {
		return {
			inherentStats: util.inherentStats[this.character.race]
		}
	},
	methods: {
		modifier (stat, type) {
			let res = Math.floor(
				(stat + (this.inherentStats[type]
					? this.inherentStats[type]
					: 0)
				) / 2) - 5
			return res
		},
		total (stat, type) {
			let res = stat
			res += this.inherentStats[type]
				? this.inherentStats[type]
				: 0
			res += this.enhanceStats[type]
				? this.enhanceStats[type]
				: 0
			res += this.miscellaneousStats[type]
				? this.miscellaneousStats[type]
				: 0
			return res
		}
	},
	props: {
		character: {
			type: Object,
			default: function () {
				return {
					stats: {
						str: 10,
						dex: 18,
						con: 10,
						int: 12,
						wis: 12,
						cha: 17
					},
					race: 'catfolk',
				}
			}
		},
		elevation: {
			type: Number,
			default: 7
		},
		enhanceStats: {
			type: Object,
			default: function () {
				return {}
			}
		},
		miscellaneousStats: {
			type: Object,
			default: function () {
				return {}
			}
		},
	}
}
</script>
