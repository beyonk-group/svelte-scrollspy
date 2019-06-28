<span class:active={activeSectionId === id}>
	<slot></slot>
</span>

<script>
	export let activeSectionId
	export let id
</script>