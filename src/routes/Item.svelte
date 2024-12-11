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
</script>

<div class='group relative flex items-center gap-8 px-8 py-8 bg-white rounded-4xl'>
    <p class='flex justify-center items-center size-16 rounded-full bg-black text-white font-bold'>{place}</p>
    <p class='mr-auto font-bold'>{name}</p>
    <p class='text-6xl font-bold'>
        {
          new Intl.NumberFormat('en-CA', {
            style: 'currency',
            currency: 'CAD',
          }).format(score)
        }
    </p>
    <div class='absolute left-[calc(100%+16px)] flex space-x-2 opacity-0 group-hover:opacity-100 transition duration-50'>
        <button class='flex justify-center items-center size-10 rounded-full text-white/50' onclick={update}>
            +
        </button>
        <button class='flex justify-center items-center size-10 rounded-full text-white/50' onclick={remove}>
            ×
        </button>
    </div>
</div>