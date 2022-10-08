<script>
  export let img;
  export let headerText;
</script>

<header>
  <h1>{headerText}</h1>
  <img src={img} alt={headerText} />
</header>

<style>
  img {
    height: 100%;
    width: 100%;
    background-size: contain;
  }

  header {
    position: relative;
    display: grid;
    place-items: center;
    width: 100vw;
    height: max(60vh, 500px);
    overflow: hidden;
    background: var(--background-image);
    background-size: contain;
    background-repeat: no-repeat;
    margin-bottom: 1rem;
    aspect-ratio: 16 / 9;
  }

  header::before {
    content: "";
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    width: 100%;
    height: 100%;
    background: #0009;
  }

  h1 {
    position: absolute;
    width: 80vw;
    text-align: center;
    top: 50%;
    left: 50%;
    color: #eee;
    transform: translate(-50%, -50%);
    font-size: clamp(2rem, 10vw, 5rem);
    margin: 0;
    padding: 0;
    font-family: "Lucida Sans", "Lucida Sans Regular", "Lucida Grande",
      "Lucida Sans Unicode", Geneva, Verdana, sans-serif;
    text-shadow: 0 0 10px #000;
  }
</style>
