
<div class="beyonk-svelte-scrollspy" bind:this={container}>
	<slot></slot>
</div>

<script>
	import { onMount } from 'svelte'

	export let activeSectionId
	
	let sections
	let container
	let visible = []
	let io

	onMount(() => {
		const sectionElements = [].slice.call(container.querySelectorAll('.scrollable-section'))
		sections = sectionElements.map(s => s.id)

		io = new IntersectionObserver(entries => {
			entries.forEach(e => {
				const id = e.target.id
				if (e.isIntersecting) {
					const op = sections.indexOf(id) < sections.indexOf(visible[0]) ? 'unshift' : 'push'
					visible[op](id)
				} else {
					const visiblePosition = visible.indexOf(id)
					visiblePosition > -1 && visible.splice(visiblePosition, 1)
				}
			})

			activeSectionId = visible[0]
		}, { threshold: [ 1 ] })

		sectionElements.forEach(el => {
			io.observe(el)
		})

		return () => io.disconnect()
	})
</script>