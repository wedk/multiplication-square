<script>
  export let calculations;

  let square = [];

  $: {
    const sideLength = Math.sqrt(calculations.length);
    const nextSquare = new Array(sideLength);
    for (let i = 0; i < nextSquare.length; i++) {
      const start = i * sideLength;
      const end = start + sideLength;
      nextSquare[i] = calculations.slice(start, end);
    }
    square = nextSquare;
  }
</script>

<style>
  table {
    border-collapse: collapse;
  }

  th,
  td {
    border: 1px solid var(--border);
    width: 27px;
    height: 27px;
    text-align: center;
  }

  th {
    background-color: var(--accent-background);
    font-weight: bold;
  }

  .main-diagonal {
    background-color: var(--primary);
  }
</style>

<table>
  <tr>
    <th>&times;</th>
    {#each square as row, index}
      <th>{index + 1}</th>
    {/each}
  </tr>
  {#each square as row, index}
    <tr>
      <th>{index + 1}</th>
      {#each row as cell, cellIndex}
        <td class:main-diagonal={cellIndex == index}>{cell || ''}</td>
      {/each}
    </tr>
  {/each}
</table>
