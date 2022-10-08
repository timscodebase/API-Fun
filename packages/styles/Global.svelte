<script>
  export let backgroundColor = "#111";

  function cssVariables(node, variables) {
    setCssVariables(node, variables);

    return {
      update(variables) {
        setCssVariables(node, variables);
      },
    };
  }
  function setCssVariables(node, variables) {
    for (const name in variables) {
      node.style.setProperty(`--${name}`, variables[name]);
    }
  }
</script>

<svelte:head>
  <style>
    html {
      -moz-text-size-adjust: none;
      -webkit-text-size-adjust: none;
      text-size-adjust: none;
    }

    body {
      /* background: var(--background-color); */
      font-family: Arial, Helvetica, sans-serif;
      margin: 0;
    }

    *:where(:not(iframe, canvas, img, svg, video):not(svg *)) {
      all: unset;
      display: revert;
    }

    *,
    *::before,
    *::after {
      box-sizing: border-box;
    }

    ol,
    ul {
      list-style: none;
    }

    img {
      max-width: 100%;
    }

    h2 {
      font-size: clamp(2rem, 4vw, 3rem);
      padding: 0.5rem 0;
    }

    p {
      padding-bottom: 0.5rem;
    }

    nav {
      display: grid;
      place-items: center;
    }

    .content {
      padding: 1rem;
    }

    /* .card:has(> img) {
      width: 100%;
      height: 200px;
      object-fit: cover;
      border-radius: 0.5rem 0.5rem 0 0;
    } */

    table {
      border-collapse: collapse;
    }

    textarea {
      white-space: revert;
    }
  </style>
</svelte:head>

<div use:cssVariables={{ backgroundColor }}>
  <slot />
</div>

<style>
  div {
    width: 100%;
    height: 100%;
    background-color: var(--backgroundColor);
  }
</style>
