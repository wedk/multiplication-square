<script>
  import { onMount } from 'svelte';

  import CalculationForm from './CalculationForm.svelte';
  import MultiplicationSquare from './MultiplicationSquare.svelte';
  import Notice from './Notice.svelte';

  const calculations = new Array(12 * 12).fill(null);

  let calculationIndex;
  $: calculationLeftTerm = Math.floor(calculationIndex / 12) + 1;
  $: calculationRightTerm = (calculationIndex % 12) + 1;

  $: remainingCalcuationsIndexes = calculations.reduce((acc, result, index) => {
    if (result == null) {
      acc.push(index);
    }
    return acc;
  }, []);

  onMount(() => {
    nextCalculation();
  });

  function nextCalculation() {
    calculationIndex =
      remainingCalcuationsIndexes[
        Math.floor(Math.random() * remainingCalcuationsIndexes.length)
      ];
  }

  function handleOnAnswer(ev) {
    calculations[calculationIndex] = ev.detail.result;
    nextCalculation();
  }
</script>

<style>
  h2 {
    line-height: 51px;
    margin-bottom: 14px;
    margin-top: 0;
    text-align: center;
  }
</style>

{#if remainingCalcuationsIndexes.length}
  <CalculationForm
    leftTerm={calculationLeftTerm}
    rightTerm={calculationRightTerm}
    on:answer={handleOnAnswer}
    on:skip={nextCalculation} />
{:else}
  <h2>Congratulations!</h2>
{/if}

<MultiplicationSquare {calculations} />

<Notice />
