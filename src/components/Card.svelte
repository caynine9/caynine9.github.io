<script lang="ts">
  export let title: string;
  export let description: string;
  export let date: Date;
  export let url: string;
  export let coverImage: string | undefined = undefined;

  $: formattedDate = new Date(date).toLocaleDateString('en-us', {
    year: 'numeric',
    month: 'short',
    day: 'numeric',
  });
</script>

<a href={url} class="group block no-underline">
  <article class="glass rounded-2xl overflow-hidden transition-transform duration-300 hover:scale-[1.02] active:scale-95 flex flex-col h-full">
    {#if coverImage}
      <div class="aspect-[16/9] w-full overflow-hidden bg-gray-100 dark:bg-gray-800">
        <img src={coverImage} alt={title} class="w-full h-full object-cover" />
      </div>
    {/if}
    <div class="p-6 flex flex-col flex-grow">
      <time class="text-xs font-medium uppercase tracking-wider opacity-60 mb-2">{formattedDate}</time>
      <h2 class="text-xl font-bold leading-tight mb-3 group-hover:text-blue-500 transition-colors">{title}</h2>
      <p class="text-sm opacity-80 line-clamp-3 mt-auto">{description}</p>
    </div>
  </article>
</a>
