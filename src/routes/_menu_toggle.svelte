<script>
  export let open = false;
</script>

<button class:open on:click={() => (open = !open)}>
  <span class="text">
    {#if open}
      Close menu
    {:else}
      Open menu
    {/if}
  </span>
  <span class="top" />
  <span class="bottom" />
  <span class="clockwise" />
  <span class="counterwise" />
</button>

<style>
  button {
    z-index: 4;
    cursor: pointer;
    appearance: none;
    position: fixed;
    left: 0;
    top: 0;
    width: 80px;
    height: 80px;
    border: none;
    border-radius: 0;
    background: none;
    outline: none;
    opacity: 0.5;
    transition: opacity 0.25s ease;
  }

  button:active {
    background: none;
  }

  button:focus {
    opacity: 1;
  }

  @media (hover: hover) {
    button:hover {
      opacity: 1;
    }
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

  .top,
  .bottom,
  .clockwise,
  .counterwise {
    position: absolute;
    display: block;
    height: 2px;
    width: 30%;
    left: 35%;
    top: calc(50% - 1px);
    background-color: var(--color-text);
    border-radius: 999em;
  }

  .top {
    transform: translateY(-7px);
  }
  .bottom {
    transform: translateY(7px);
  }
  .top,
  .bottom {
    transition: transform 150ms cubic-bezier(0, 0, 0.2, 1) 150ms, opacity 0ms 150ms,
      background-color var(--color-transition);
  }
  .open .top,
  .open .bottom {
    opacity: 0;
    transform: translateY(0);
    transition: transform 150ms cubic-bezier(0.4, 0, 1, 1), opacity 0ms 150ms,
      background-color var(--color-transition);
  }

  .clockwise,
  .counterwise {
    transition: transform 150ms cubic-bezier(0.4, 0, 1, 1), background-color var(--color-transition);
  }
  .open .clockwise,
  .open .counterwise {
    transition: transform 150ms cubic-bezier(0, 0, 0.2, 1) 150ms,
      background-color var(--color-transition);
  }
  .open .clockwise {
    transform: rotate(45deg);
  }
  .open .counterwise {
    transform: rotate(-45deg);
  }

  @media print {
    button {
      display: none;
    }
  }
</style>
