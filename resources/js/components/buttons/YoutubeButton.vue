<template>
	<base-button
		:isDisabled="mode != 'editor'"
		:clickMethod="addYoutube"
		:icon="['fas', 'play']"
		title="Insert YouTube video"
	>
	</base-button>
</template>

<script>
	import BaseButton from "./BaseButton.vue";

	export default {
		components: { BaseButton },
		props: [
		    'editor',
			'mode'
		],

		data: function() {
			return {

			}
		},

		mounted() {

		},

		methods: {
			addYoutube() {
				const url = window.prompt('Paste a YouTube URL')

				if (!url) {
					return;
				}

				const clean = this.normalizeYoutubeUrl(url)
				this.editor?.commands.setYoutubeVideo({ src: clean })
			},

			normalizeYoutubeUrl(url) {
				try {
					const u = new URL(url.trim());

					if (u.hostname.includes('youtu.be')) {
						return `https://www.youtube.com/watch?v=${u.pathname.slice(1)}`
					}

					return url;
				} catch {
					return url;
				}
			}
		},

		computed: {

		}
	}
</script>