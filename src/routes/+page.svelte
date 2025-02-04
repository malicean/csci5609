<script>
  let maxClick = $state(6);

  // Ignoring error cus I just want to reference current value
  // svelte-ignore state_referenced_locally
  let prevMaxClick = maxClick;

  // svelte-ignore state_referenced_locally
  let cnt = $state(maxClick);

  function onClick() {
    cnt -= 1;
  }
</script>

<h1>Alison Janik's VIS Site</h1>

<img
  width="600px"
  src="https://upload.wikimedia.org/wikipedia/commons/3/38/Base-catalysed_aldol_condensation.svg"
  alt="Mechanism of a base-catalyzed aldol condensation"
/>

<div>
  You can click up to
  <select
    bind:value={maxClick}
    onchange={() => {
      // not sure how to do this without intermediate state of prevMaxClick
      // but also this is my first time doing web development so maybe I'm just an idiot
      cnt += maxClick - prevMaxClick;
      prevMaxClick = maxClick;
    }}
  >
    {#each [2, 4, 6] as optionNum}
      <option value={optionNum}>
        {optionNum}
      </option>
    {/each}
  </select>
  times
</div>
<button onclick={onClick}> Click Me </button>

{#if cnt > 0}
  <p id="info">Remaining Number of Clicks: {cnt}</p>
{:else}
  <p>No more clicks allowed</p>
{/if}

<style>
  body {
    font-family: Helvetica, Arial, sans-serif;
  }
  button {
    background-color: #44aa66;
    /* background-color: blue; */
    color: white;
    font-size: xx-large;
    padding: 10px 20px;
    border: none;
    cursor: pointer;
    border-radius: 5px;
  }
</style>
