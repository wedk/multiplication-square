<script>
  import { createEventDispatcher } from 'svelte';

  const dispatch = createEventDispatcher();

  export let leftTerm;
  export let rightTerm;
  export let result = '';

  let error = false;

  function handleSubmit() {
    const resultAsInt = parseInt(result, 10);
    if (leftTerm * rightTerm === resultAsInt) {
      error = false;
      dispatch('answer', {
        result: resultAsInt
      });
    } else {
      error = true;
    }
  }

  function handleSkip(ev) {
    if (ev.key === 'ArrowDown' || ev.key == 'ArrowUp') {
      ev.preventDefault();
      dispatch('skip');
    }
  }

  function reset() {
    result = '';
    error = false;
  }

  $: reset(leftTerm, rightTerm);
</script>

<style>
  form {
    font-size: 1.75rem;
    text-align: center;
    padding: 0.25em;
    margin-bottom: 0.5em;
  }

  input {
    background: var(--accent-background);
    border: 1px solid var(--border);
    color: var(--foreground);
    font-size: 1.75rem;
    text-align: center;
  }

  .error {
    color: brown;
    font-size: 0.9em;
  }
</style>

<form on:submit|preventDefault={handleSubmit}>
  <b>{leftTerm}</b>
  &times;
  <b>{rightTerm}</b>
  =
  <input type="text" size="4" aria-label="Result" bind:value={result} on:keydown={handleSkip} />
  {#if error }
    <b class="error">&#9888;</b>
  {/if}
</form>
