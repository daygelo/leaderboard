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

<main class='w-full min-h-screen bg-yellow-500 text-4xl'>
  <section class='w-full max-w-4xl mx-auto py-32'>
    <div>
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

    <input
      class='w-full mt-8 text-white outline-none placeholder:text-white/0 hover:placeholder:text-white/25 placeholder:transition'
      placeholder='type here'
      bind:value={inputValue}
      onkeyup={event => {
        if (event.key === 'Enter') {
          items[nanoid()] = { name: inputValue, score: 0 };
          inputValue = '';
        }
      }}
    />
  </section>
</main>