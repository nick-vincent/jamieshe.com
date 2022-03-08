<script lang="ts">
  import { navigating } from '$app/stores';

  import Nav from './_nav.svelte';
  import '../app.css';

  let navOpen = false;
  let main: HTMLElement;

  const blurDuration = 500;
  const slideDuration = 500;

  const transitionStyles = `--blur-duration: ${blurDuration}ms; --slide-duration: ${slideDuration}ms`;

  $: if (main && $navigating) {
    main.scrollTo({ top: 0 });
  }

  $: if (main) {
    main.querySelectorAll('a').forEach((a) => (a.tabIndex = navOpen ? -1 : 0));
  }
</script>

<Nav bind:open={navOpen} duration={slideDuration} delay={blurDuration / 2} />

<main bind:this={main} class:navOpen style={transitionStyles}>
  <div class="content">
    <slot />
  </div>
</main>

<style>
  main {
    --gradientMask: linear-gradient(
      to bottom,
      transparent 3em,
      black 7em,
      black calc(100% - 4em),
      transparent 100%
    );
    z-index: 2;
    overflow-y: scroll;
    position: fixed;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    padding: 6em 1em;
    mask-image: var(--gradientMask);
    -webkit-mask-image: var(--gradientMask);
    transform-origin: center;
    transition-property: opacity, filter, transform;
    transition-duration: var(--blur-duration);
    transition-timing-function: ease-in-out;
    transition-delay: var(--slide-duration);
  }

  main.navOpen {
    opacity: 0;
    filter: blur(1em);
    transform: scale(0.95);
    transition-delay: 0ms;
  }

  .content {
    max-width: 25em;
    min-height: 100%;
    margin: 0 auto;
    display: flex;
    flex-direction: column;
    place-content: center;
  }

  @media print {
    main {
      position: static;
      padding: 0;
      mask-image: none;
      -webkit-mask-image: none;
    }
    .content {
      max-width: none;
    }
  }
</style>
