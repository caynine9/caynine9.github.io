<script lang="ts">
  import { GithubLogo, LinkedinLogo, EnvelopeSimple, CaretUp } from "phosphor-svelte";
  const today = new Date();
</script>

<footer class="py-16 mt-16 border-t border-[var(--border)] relative overflow-hidden bg-[var(--bg)]">
  <div class="max-w-5xl mx-auto px-5 relative z-10 flex flex-col md:flex-row items-center justify-between gap-8">
    
    <div class="flex flex-col items-center md:items-start gap-4">
      <p class="text-xs font-mono text-[var(--subtle)]">
        &copy; {today.getFullYear()} Muhammad Tantowi Jauhari
      </p>
    </div>

    <div class="flex items-center gap-6">
      <a href="https://github.com/caynine9" target="_blank" rel="noopener noreferrer" class="text-[var(--subtle)] hover:text-[var(--text)] transition-colors hover:-translate-y-0.5 duration-300" aria-label="GitHub">
        <GithubLogo size={24} weight="regular" />
      </a>
      <a href="https://linkedin.com/in/mtantowij" target="_blank" rel="noopener noreferrer" class="text-[var(--subtle)] hover:text-[var(--accent)] transition-colors hover:-translate-y-0.5 duration-300" aria-label="LinkedIn">
        <LinkedinLogo size={24} weight="regular" />
      </a>
      <a href="mailto:tantowijauhari16@gmail.com" class="text-[var(--subtle)] hover:text-[var(--text)] transition-colors hover:-translate-y-0.5 duration-300" aria-label="Email">
        <EnvelopeSimple size={24} weight="regular" />
      </a>
    </div>

    <!-- Back to top -->
    <button on:click={() => window.scrollTo({ top: 0, behavior: 'smooth' })} class="hidden md:flex p-3 rounded-full bg-[var(--bg)] border border-[var(--border)] text-[var(--subtle)] hover:text-[var(--text)] hover:bg-[var(--accent-glow)] hover:border-[var(--accent)] transition-all hover:-translate-y-1" aria-label="Back to top">
      <CaretUp size={18} weight="bold" />
    </button>
  </div>
</footer>
