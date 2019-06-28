<p align="center">
  <img width="186" height="90" src="https://user-images.githubusercontent.com/218949/44782765-377e7c80-ab80-11e8-9dd8-fce0e37c235b.png" alt="Beyonk" />
</p>

## Svelte Scroll Spy

[![js-standard-style](https://img.shields.io/badge/code%20style-standard-brightgreen.svg)](http://standardjs.com) [![CircleCI](https://circleci.com/gh/beyonk-adventures/svelte-scrollspy.svg?style=shield)](https://circleci.com/gh/beyonk-adventures/svelte-scrollspy) [![svelte-v2](https://img.shields.io/badge/svelte-v2-orange.svg)](https://v2.svelte.dev) [![svelte-v3](https://img.shields.io/badge/svelte-v3-blueviolet.svg)](https://svelte.dev)

Svelte Scroll Spy component

This component uses IntersectionObservers (and a polyfill for non-supporting browsers like Safari) so that performance is quick and doesn't impact the user's experience.

## Usage

This library is pure javascript, so can be used with any framework you like.

### Demo

```
npm run dev // http://localhost:12001
```

### To use within a Svelte application:

```bash
npm i -D @beyonk/svelte-scrollspy
```

## Usage

```jsx
<ScrollSpy>
  <ul>
    {#each sections as section (section.id)}
    <li>
      <SectionHeader id="{section.id}">
        {section.title}
      </SectionHeader>
    </li>
    {/each}
  </ul>
  {#each sections as section (section.id)}
  <ScrollableSection id="{section.id}">
    <h2>{section.title}</h2>
    <p>{section.content}</p>
  </ScrollableSection>
  {/each}
</ScrollSpy>

<script>
  import { SectionHeader, ScrollableSection, ScrollSpy } from '@beyonk/svelte-scrollspy'

  let activeSectionId: undefined
  const sections = [
    { id: 'abc', title: 'Some Title', content: 'Lorem ipsum dolor...' },
    { id: 'def', title: 'Some Other Title', content: 'Lorem ipsum dolor...' },
    { id: 'ghi', title: 'A Different Title', content: 'Lorem ipsum dolor...' }
  ]
</script>
```

You need to set id on each `ScrollableHeader` and its corresponding `ScrollableSection`. Besides that, everything else is pretty freeform.

Upon scrolling to the appropriate section of the page, the heading of the section which is topmost visible on the page will get the class 'active'.

Therefore, you could indicate the current section in the example above by highlighting it in red as follows:

```html
<style>
	:global(.beyonk-svelte-scrollspy .active) {
		color: red;
	}
</style>
```
