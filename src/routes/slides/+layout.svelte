<script>
	import { onMount } from 'svelte';
	import Reveal from 'reveal.js';
	import RevealNotes from 'reveal.js/plugin/notes/notes';
	import RevealHighlight from 'reveal.js/plugin/highlight/highlight';

	import 'reveal.js/dist/reveal.css';
	import 'reveal.js/dist/theme/black.css';
	import 'reveal.js/plugin/highlight/monokai.css';

	onMount(() => {
		Reveal.initialize({
			controls: true,
			progress: true,
			center: true,
			hash: true,

			// Learn about plugins: https://revealjs.com/plugins/
			plugins: [RevealNotes, RevealHighlight]
		});
	});
</script>

<div class="reveal">
	<!-- Any section element inside of this container is displayed as a slide -->
	<div class="slides">
		<slot />
	</div>
</div>
