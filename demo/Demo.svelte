<script>
  import { ScrollSpy, SectionHeader, ScrollableSection } from '../src/index.js'
  import Chance from 'chance'

  const chance = Chance()

  const sections = new Array(chance.integer({ min: 6, max: 20 })).fill(0).map(s => ({
    title: chance.sentence({ words: chance.integer({ min: 1, max: 5 }) }),
    id: chance.hash(),
    text: new Array(chance.integer({ min: 1, max: 10 })).fill(0).map(p => ([
      '<p>',
      chance.paragraph({ sentences: chance.integer({ min: 1, max: 10 }) }),
      '</p>'
    ].join(''))).join('')
  }))
</script>

<ScrollSpy {sections}>
  <div class="columns">
    <div class="left column">
      <ul>
        {#each sections as section}
        <li>
          <SectionHeader id={section.id}>
            <a href="#{section.id}">{section.title}</a>
          </SectionHeader>
        </li>
        {/each}
      </ul>
    </div>
    <div class="right column">
      {#each sections as section (section.id)}
      <ScrollableSection id="{section.id}">
        <h4>{section.title}</h4>
        {@html section.text}
      </ScrollableSection>
      {/each}
    </div>
  </div>
</ScrollSpy>

<style>
  .columns {
    display: flex;
  }

  .column {
    font-family: sans-serif;
    padding: 2vh 2vw;
  }

  ul {
    list-style-type: none;
  }

  li {
    padding: 1vh 0.25vw;
  }

  a, a:hover, a:active, a:visited {
    color: darkslategrey;
    text-decoration: none;
  }

  h4 {
    padding-top: 2vh;
  }

  .left {
    position: fixed;
    top: 0;
    width: 20vw;
    background-color: goldenrod;
    color: darkslategrey;
    font-weight: 700;
    font-size: 1.25rem;
  }

  .right {
    flex: 1;
    padding-left: 26vw;
  }

  :global(.beyonk-svelte-scrollspy .active a) {
    color: cornflowerblue;
  }

  :global(.beyonk-svelte-scrollspy .scrollable-section) {
    min-height: 100vh;
  }
</style>