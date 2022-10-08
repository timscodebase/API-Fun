<script>
  export let active = false;
  export let callback = () => {};
</script>

<button on:click={callback} class={active ? "active" : ""}><slot /></button>

<style>
  button {
    padding: 0.5rem 1rem;
    margin: 1rem 0;
    border: none;
    border-radius: 0.5rem;
    color: #eee;
    font-size: 1.5rem;
    cursor: pointer;
    background: #0000;
    border: 1px solid #eee;
  }

  .active {
    font-weight: bold;
    border: 2px solid #eee;
  }
</style>
