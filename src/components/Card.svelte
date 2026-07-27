<script lang="ts">
  export let title: string;
  export let description: string;
  export let date: Date;
  export let url: string;
  export let coverImage: string | undefined = undefined;

  // Approximate reading time (assuming ~250 words per minute).
  // In a real scenario, this would be passed as a prop from the markdown frontmatter,
  // but we'll create a nice placeholder for the UI for now.
  const readingTime = Math.max(3, Math.ceil(description.split(" ").length / 5));

  $: formattedDate = new Date(date).toLocaleDateString('en-us', {
    year: 'numeric',
    month: 'short',
    day: 'numeric',
  });
</script>

<a href={url} class="group block no-underline h-full outline-none focus-visible:ring-2 focus-visible:ring-[var(--accent)] rounded-2xl">
  <article class="card-elevated overflow-hidden flex flex-col h-full bg-[var(--card)] group-hover:border-[var(--accent)] transition-all duration-500">
    {#if coverImage}
      <div class="relative aspect-[16/9] w-full overflow-hidden bg-black/5 dark:bg-white/5">
        <div class="absolute inset-0 bg-gradient-to-t from-[var(--card)] to-transparent z-10 opacity-60 mix-blend-multiply dark:mix-blend-screen transition-opacity group-hover:opacity-20"></div>
        <img src={coverImage} alt={title} class="w-full h-full object-cover transition-transform duration-700 group-hover:scale-105" loading="lazy" />
      </div>
    {/if}
    <div class="p-6 md:p-8 flex flex-col flex-grow relative z-20">
      <div class="flex items-center gap-3 text-[11px] font-bold uppercase tracking-widest text-[var(--subtle)] mb-4">
        <time>{formattedDate}</time>
        <span class="w-1 h-1 rounded-full bg-[var(--accent)] opacity-50"></span>
        <span>~{readingTime} min read</span>
      </div>
      <h2 class="text-xl md:text-2xl font-bold leading-tight mb-4 text-[var(--text)] group-hover:text-gradient transition-all duration-300">
        {title}
      </h2>
      <p class="text-sm md:text-base text-[var(--subtle)] line-clamp-3 mt-auto leading-relaxed">
        {description}
      </p>

      <!-- Read More Link Indicator -->
      <div class="mt-6 flex items-center gap-2 text-sm font-semibold text-[var(--accent)] opacity-0 -translate-x-2 group-hover:opacity-100 group-hover:translate-x-0 transition-all duration-300">
        Read Article 
        <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round">
          <line x1="5" y1="12" x2="19" y2="12"></line>
          <polyline points="12 5 19 12 12 19"></polyline>
        </svg>
      </div>
    </div>
  </article>
</a>
