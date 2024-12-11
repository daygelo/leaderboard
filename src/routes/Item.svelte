<script lang='ts'>
    let {
      place,
      name,
      score,
      update,
      remove,
    }: {
      place: number,
      name: string,
      score: number,
      update: () => void,
      remove: () => void,
    } = $props();

    const placeStyle = $derived(place === 1 ? 'text-amber-500' : place === 2 ? 'text-slate-400' : place === 3 ? 'text-red-500' : 'text-gray-700');
</script>

<div class='group relative flex items-center gap-12 px-8 py-8 text-6xl'>
    <p class={`flex justify-center items-center size-16 rounded-full ${placeStyle} text-8xl font-array font-bold`}>{place}</p>
    <p class='mr-auto'>{name}</p>
    <p class='font-array font-bold'>
        {
          new Intl.NumberFormat('en-CA', {
            style: 'currency',
            currency: 'CAD',
          }).format(score)
        }
    </p>
    <div class='absolute left-[calc(100%+16px)] flex space-x-2 opacity-0 group-hover:opacity-100 transition duration-50 text-4xl'>
        <button class='flex justify-center items-center size-10 rounded-full text-white/50' onclick={update}>
            +
        </button>
        <button class='flex justify-center items-center size-10 rounded-full text-white/50' onclick={remove}>
            ×
        </button>
    </div>
</div>