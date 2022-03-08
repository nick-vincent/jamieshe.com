<svelte:head>
  <title>Jamie She: About</title>
  <meta
    name="description"
    content="Jamie is a multicultural user experience researcher, museum fiend, and theme park enthusiast."
  />
</svelte:head>

<div>
  <h1>About</h1>
  <a href="/JamieShe.jpg" target="_blank"
    ><img alt="Portrait of Jamie She" src="/JamieShe_750x999.jpg" width="750" height="999" /></a
  >
  <p>
    Jamie is a multicultural user experience researcher, museum fiend, and theme park enthusiast.
  </p>
  <p>
    Growing up as a global nomad fueled her desire to understand and explore the human experience.
    After country hopping for years with jobs that have taken her to strange corners of the world,
    she moved to San Francisco to attend UC Berkeley with a focus in consciousness, philosophy of
    science, and social cognition.
  </p>
  <p>
    Jamie now leverages her 15-year background in experience-centric industries and endless
    curiosity to understand and improve how people interact with intelligent technology.
  </p>
  <p>
    Outside of work, you’ll find her befriending robots, prowling flea markets, knitting kitten
    mittens, and visiting tiki bars around the world.
  </p>
</div>

<style>
  a {
    display: block;
    overflow: hidden;
    clip-path: content-box;
    border-radius: 1em;
    margin: 1em 0 0;
    width: 100%;
    background: none;
  }

  img {
    display: block;
    width: 100%;
    height: auto;
    transition: transform 1s ease;
  }

  a:focus img {
    transform: scale(1.05);
  }

  @media (hover: hover) {
    a:hover img {
      transform: scale(1.05);
    }
  }

  @media print, (min-width: 480px) {
    a {
      margin: 1em 1em 0.5em 0;
      float: left;
      width: calc(50% - 0.5em);
    }
  }
</style>
