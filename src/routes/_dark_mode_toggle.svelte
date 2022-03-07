<script>
  import { onMount } from 'svelte';

  const STORAGE_KEY = 'theme';
  const DARK_PREFERENCE = '(prefers-color-scheme: dark)';
  const THEMES = {
    DARK: 'dark',
    LIGHT: 'light'
  };

  let darkMode;

  onMount(() => {
    applyTheme();
    window.matchMedia(DARK_PREFERENCE).addEventListener('change', applyTheme);
  });

  const prefersDarkThemes = () => window.matchMedia(DARK_PREFERENCE).matches;

  const toggleTheme = () => {
    const stored = localStorage.getItem(STORAGE_KEY);

    if (stored) {
      // clear storage
      localStorage.removeItem(STORAGE_KEY);
    } else {
      // store opposite of preference
      localStorage.setItem(STORAGE_KEY, prefersDarkThemes() ? THEMES.LIGHT : THEMES.DARK);
    }

    applyTheme();
  };

  const applyTheme = () => {
    const preferredTheme = prefersDarkThemes() ? THEMES.DARK : THEMES.LIGHT;
    const currentTheme = localStorage.getItem(STORAGE_KEY) ?? preferredTheme;

    if (currentTheme === THEMES.DARK) {
      darkMode = true;
      document.documentElement.classList.remove(THEMES.LIGHT);
      document.documentElement.classList.add(THEMES.DARK);
    } else {
      darkMode = false;
      document.documentElement.classList.remove(THEMES.DARK);
      document.documentElement.classList.add(THEMES.LIGHT);
    }
  };
</script>

<button class:darkMode on:click={toggleTheme}>
  <span class="text">
    {#if darkMode}
      Switch to light mode
    {:else}
      Switch to dark mode
    {/if}
  </span>
  <span class="circle">
    <span class="left" />
    <span class="right" />
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

  .darkMode .circle {
    transform: rotate(180deg);
  }

  .left,
  .right {
    display: block;
    position: absolute;
    width: 8px;
    height: 20px;
    top: 0;
    transition: background-color var(--color-transition);
  }

  .left {
    left: 0;
    background-color: var(--color-white);
  }

  .right {
    right: 0;
    background-color: var(--color-black);
  }

  @media print {
    button {
      display: none;
    }
  }
</style>
