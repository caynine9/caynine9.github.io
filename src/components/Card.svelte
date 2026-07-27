<script lang="ts">
  import { ArrowRight } from "phosphor-svelte";
  
  export let title: string;
  export let description: string;
  export let date: Date;
  export let url: string;
  export let coverImage: string | undefined = undefined;
  export let lang: string = "en";

  // Approximate reading time (assuming ~250 words per minute).
  const readingTime = Math.max(3, Math.ceil(description.split(" ").length / 5));

  $: formattedDate = new Date(date).toLocaleDateString(lang === 'id' ? 'id-ID' : 'en-US', {
    year: 'numeric',
    month: 'short',
    day: 'numeric',
  });
</script>

<a href={url} class="group block no-underline h-full outline-none focus-visible:ring-2 focus-visible:ring-[var(--accent)] rounded-2xl">
  <article class="card-elevated overflow-hidden flex flex-col h-full bg-[var(--card)] border-[var(--border)] group-hover:border-[var(--accent)] transition-all duration-300">
    {#if coverImage}
      <div class="relative aspect-[16/9] w-full overflow-hidden bg-black/5 dark:bg-white/5">
        <div class="absolute inset-0 bg-gradient-to-t from-[var(--card)] to-transparent z-10 opacity-60 mix-blend-multiply dark:mix-blend-screen transition-opacity group-hover:opacity-10"></div>
        <img src={coverImage} alt={title} class="w-full h-full object-cover transition-transform duration-700 ease-out group-hover:scale-105" loading="lazy" decoding="async" />
      </div>
    {/if}
    <div class="p-6 md:p-8 flex flex-col flex-grow relative z-20">
      <div class="flex items-center gap-3 text-xs font-mono font-medium uppercase tracking-widest text-[var(--subtle)] mb-4">
        <time>{formattedDate}</time>
        <span class="w-1 h-1 rounded-full bg-[var(--accent)] opacity-50"></span>
        <span>~{readingTime} min read</span>
      </div>
      <h2 class="text-xl md:text-2xl font-bold leading-tight mb-4 text-[var(--text)] transition-colors duration-300 break-words group-hover:text-[var(--accent)]">
        {title}
      </h2>
      <p class="text-sm md:text-base text-[var(--subtle)] line-clamp-3 mt-auto leading-relaxed max-w-[65ch]">
        {description}
      </p>

      <!-- Read More Link Indicator -->
      <div class="mt-6 flex items-center gap-2 text-sm font-semibold text-[var(--accent)] opacity-0 -translate-x-2 group-hover:opacity-100 group-hover:translate-x-0 transition-all duration-300">
        Read Article 
        <ArrowRight size={16} weight="bold" />
      </div>
    </div>
  </article>
</a>
