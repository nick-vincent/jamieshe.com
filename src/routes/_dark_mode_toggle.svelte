<script>
  import { afterUpdate } from 'svelte';
  import DarkMode from 'svelte-dark-mode';

  let theme = 'light';

  $: switchTheme = theme === 'dark' ? 'light' : 'dark';

  afterUpdate(() => {
    document.documentElement.className = theme; // "dark" or "light"
  });
</script>

<DarkMode bind:theme />

<button on:click={() => (theme = switchTheme)}>
  <span class="text">
    Switch to {switchTheme} mode
  </span>
  <span class="circle {theme}">
    <span class="top" />
    <span class="bottom" />
  </span>
</button>

<style>
  button {
    z-index: 4;
    cursor: pointer;
    appearance: none;
    position: fixed;
    right: 0;
    top: 0;
    width: 80px;
    height: 80px;
    border: none;
    border-radius: 0;
    background: none;
    outline: none;
  }

  button:active {
    background: none;
  }

  .text {
    clip: rect(0 0 0 0);
    clip-path: inset(50%);
    height: 1px;
    overflow: hidden;
    position: absolute;
    white-space: nowrap;
    width: 1px;
  }

  .circle {
    display: block;
    position: absolute;
    overflow: hidden;
    width: 20px;
    height: 20px;
    left: 30px;
    top: 30px;
    border: 2px solid var(--color-text);
    border-radius: 50%;
    transition: border-color var(--color-transition), transform var(--color-transition);
  }

  .circle.light {
    transform: rotate(-90deg);
  }

  .circle.dark {
    transform: rotate(90deg);
  }

  .top,
  .bottom {
    display: block;
    position: absolute;
    width: 16px;
    height: 8px;
    left: 0;
  }

  .top {
    top: 0;
    background-color: var(--color-white);
  }

  .bottom {
    bottom: 0;
    background-color: var(--color-black);
  }

  @media print {
    button {
      display: none;
    }
  }
</style>
