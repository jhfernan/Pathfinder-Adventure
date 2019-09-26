<template>
	<v-container>
		<h1>Hello World</h1>
	</v-container>
</template>

<script>

export default {
	asyncData ({ app, error }) {
		return app.$axios.$get('/info.json')
		.then(res => {
			return { character: res }
		})
		.catch(err => { error({ statusCode: '404', message: 'Could not find Character info' }) })
	},
}
</script>
