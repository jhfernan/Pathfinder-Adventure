<template>
	<v-app dark>
		<v-container fluid fill-height>
		<v-layout align-center justify-center>
			<v-flex xs12 sm8 md6 lg4>
				<v-card class="elevation-12">
					<v-card-text>
						<div class="headline mb-2">
							<h1 v-if="!error.statusCode">Error</h1>
							<h1 v-else>{{ error.statusCode }}</h1>
						</div>
						<div>
							{{ error.message ? error.message : 'Something went wrong' }}
						</div>
						<v-card-actions>
							<v-spacer />
							<v-btn icon to="/">
								<v-icon>mdi-home</v-icon>
							</v-btn>
						</v-card-actions>
					</v-card-text>
				</v-card>
			</v-flex>
		</v-layout>
	</v-container>
		<v-container>

		</v-container>
	</v-app>
</template>

<script>
export default {
	layout: 'empty',
	props: {
		error: {
			type: Object,
			default: null
		}
	},
	head () {
		const title = this.error.statusCode === 404 ? this.pageNotFound : this.otherError
		return {
			title
		}
	},
	data () {
		return {
			pageNotFound: '404 Not Found',
			otherError: 'An error occurred'
		}
	}
}
</script>
