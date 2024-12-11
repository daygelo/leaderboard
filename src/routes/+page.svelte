<script lang='ts'>
  import Item from './Item.svelte';
  import { nanoid } from 'nanoid';
  import { flip } from 'svelte/animate';

  type ItemData = {
    name: string,
    score: number,
  }

  const items: { [key: string]: ItemData } = $state({});
  let inputValue: string = $state('');
  let increment: number = $derived(inputValue.match(/^-?\d+$/) || inputValue.match(/^-?\d*\.\d+$/) ? +inputValue : 0);
</script>

<svelte:head>
  <title>Leaderboard</title>
</svelte:head>

<main class='w-full min-h-screen bg-black text-white font-array select-none'>
  <input
    class='fixed left-8 mt-8 text-4xl text-green-500 outline-none placeholder:text-green-500/0 hover:placeholder:text-green-500/25 placeholder:transition'
    placeholder='type here'
    bind:value={inputValue}
    onkeyup={event => {
        if (event.key === 'Enter') {
          items[nanoid()] = { name: inputValue, score: 0 };
          inputValue = '';
        }
      }}
  />
  <section class='w-full max-w-4xl mx-auto py-32'>
    <div class='space-y-4'>
      {#each Object.entries(items).sort((a, b) => b[1].score - a[1].score) as [id, item], i (id)}
        <div animate:flip>
          <Item
            {...item}
            place={i + 1}
            update={() => {
            items[id].score += increment;
            inputValue = '';
          }}
            remove={() => {
            delete items[id];
          }}
        />
        </div>
      {/each}
    </div>

  </section>
</main>