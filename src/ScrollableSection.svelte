<section {id} class:active={$activeSectionId === id} class="scrollable-section">
  <slot></slot>
</section>

<script>
	import { activeSectionId } from './store.js'

	export let id
</script>