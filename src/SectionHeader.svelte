<span class:active={$activeSectionId === id}>
	<slot></slot>
</span>

<script>
	import { activeSectionId } from './store.js'

	export let id
</script>