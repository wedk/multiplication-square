<script>
  import { onMount } from 'svelte';

  let theme = 'light';

  $: reverseTheme = theme == 'light' ? 'dark' : 'light';

  function changeTheme() {
    theme = reverseTheme;
    document.body.className = theme;
  }

  onMount(() => {
    theme = document.body.className;
  });
</script>

<style>
  button {
    border-radius: 50%;
    border: 0;
    box-shadow: 0px 3px 4px -2px black;
    cursor: pointer;
    height: 24px;
    line-height: 1;
    text-align: center;
    width: 24px;
  }

  .dark {
    background-color: #121212;
    color: gainsboro;
  }

  .light {
    background-color: gainsboro;
    color: #121212;
  }
</style>

<button
  type="button"
  on:click={changeTheme}
  class={reverseTheme}
  title={`Toggle theme to ${reverseTheme}`}>
  {theme == 'light' ? '\u2600' : '\u263E'}
</button>
