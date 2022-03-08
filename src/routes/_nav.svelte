<script>
  import MenuToggle from './_menu_toggle.svelte';
  import DarkModeToggle from './_dark_mode_toggle.svelte';

  export let open = false;
  export let duration = 500;
  export let delay = 500;

  const navItems = [
    { text: 'Home', href: '/' },
    { text: 'About', href: '/about/' },
    { text: 'Resume', href: '/resume/' },
    { text: 'Contact', href: '/contact/' }
  ];

  const itemDuration = duration / navItems.length;

  const itemDelayIn = (i) => delay + itemDuration * i;
  const itemDelayOut = (i) => duration - itemDuration * i;
  const itemStyles = (i) => {
    return `
      --duration: ${itemDuration}ms;
      --delay-in: ${itemDelayIn(i)}ms;
      --delay-out: ${itemDelayOut(i)}ms;
    `;
  };
</script>

<MenuToggle bind:open />

<nav class:open>
  <ul>
    {#each navItems as item, i}
      <li style={itemStyles(i)}>
        <a sveltekit:prefetch href={item.href} on:click={() => (open = false)}>{item.text}</a>
      </li>
    {/each}
  </ul>
</nav>

<DarkModeToggle />

<style>
  nav {
    z-index: 3;
    pointer-events: none;
    position: fixed;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    text-align: center;
    display: flex;
    flex-direction: column;
    place-content: center;
    align-items: center;
    padding: 1em;
    font-size: 2em;
    line-height: 1.25em;
    font-weight: 700;
    letter-spacing: -0.025em;
  }

  nav.open {
    pointer-events: auto;
  }

  ul {
    display: flex;
    flex-direction: column;
    list-style: none;
    padding: 0;
    margin: 0;
  }

  li {
    opacity: 0;
    visibility: hidden;
    transform: translateX(-0.5em);
    transition: all var(--duration) ease-in-out var(--delay-out);
  }

  .open li {
    opacity: 1;
    visibility: visible;
    transform: translateX(0);
    transition: all var(--duration) ease-in-out var(--delay-in);
  }

  a {
    background: none;
    transition: opacity 0.5s ease-in-out;
  }

  nav:not(.open) a,
  ul:focus-within a:not(:focus) {
    opacity: 0.25;
  }

  @media (hover: hover) {
    ul:hover a:not(:hover) {
      opacity: 0.25;
    }
  }
</style>
