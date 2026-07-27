<script lang="ts">
  const today = new Date();
</script>

<footer class="py-20 mt-12 border-t border-[var(--border)] relative overflow-hidden">
  <!-- Subtle background glow at bottom -->
  <div class="absolute bottom-0 left-1/2 -translate-x-1/2 w-full max-w-3xl h-32 bg-[var(--accent)] opacity-[0.03] blur-3xl rounded-full pointer-events-none"></div>

  <div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8 relative z-10 flex flex-col md:flex-row items-center justify-between gap-8">
    
    <div class="flex flex-col items-center md:items-start gap-3">
      <div class="flex items-center gap-2 px-3 py-1.5 rounded-full border border-[var(--border)] bg-[rgba(var(--accent-rgb),0.05)] w-max">
        <span class="relative flex h-2 w-2">
          <span class="animate-ping absolute inline-flex h-full w-full rounded-full bg-[var(--accent)] opacity-75"></span>
          <span class="relative inline-flex rounded-full h-2 w-2 bg-[var(--accent)]"></span>
        </span>
        <span class="text-[11px] font-semibold text-[var(--text)] uppercase tracking-wider">Available for new opportunities</span>
      </div>
      <p class="text-xs font-medium text-[var(--subtle)]">
        &copy; {today.getFullYear()} Muhammad Tantowi Jauhari
      </p>
    </div>

    <div class="flex items-center gap-6">
      <a href="https://github.com/caynine9" target="_blank" rel="noopener noreferrer" class="text-[var(--subtle)] hover:text-[var(--accent)] transition-colors hover:-translate-y-0.5 duration-300" aria-label="GitHub">
        <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <path d="M15 22v-4a4.8 4.8 0 0 0-1-3.5c3 0 6-2 6-5.5.08-1.25-.27-2.48-1-3.5.28-1.15.28-2.35 0-3.5 0 0-1 0-3 1.5-2.64-.5-5.36-.5-8 0C6 2 5 2 5 2c-.3 1.15-.3 2.35 0 3.5A5.403 5.403 0 0 0 4 9c0 3.5 3 5.5 6 5.5-.39.49-.68 1.05-.85 1.65-.17.6-.22 1.23-.15 1.85v4"></path>
          <path d="M9 18c-4.51 2-5-2-7-2"></path>
        </svg>
      </a>
      <a href="https://linkedin.com/in/mtantowij" target="_blank" rel="noopener noreferrer" class="text-[var(--subtle)] hover:text-[var(--accent)] transition-colors hover:-translate-y-0.5 duration-300" aria-label="LinkedIn">
        <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <path d="M16 8a6 6 0 0 1 6 6v7h-4v-7a2 2 0 0 0-2-2 2 2 0 0 0-2 2v7h-4v-7a6 6 0 0 1 6-6z"></path>
          <rect x="2" y="9" width="4" height="12"></rect>
          <circle cx="4" cy="4" r="2"></circle>
        </svg>
      </a>
      <a href="mailto:tantowijauhari16@gmail.com" class="text-[var(--subtle)] hover:text-[var(--accent)] transition-colors hover:-translate-y-0.5 duration-300" aria-label="Email">
        <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          <path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"></path>
          <polyline points="22,6 12,13 2,6"></polyline>
        </svg>
      </a>
    </div>

    <!-- Back to top -->
    <button on:click={() => window.scrollTo({ top: 0, behavior: 'smooth' })} class="hidden md:flex p-3 rounded-full bg-[rgba(var(--accent-rgb),0.05)] border border-[var(--border)] text-[var(--accent)] hover:bg-[var(--accent)] hover:text-white transition-all hover:shadow-lg hover:shadow-[var(--accent-glow)]" aria-label="Back to top">
      <svg xmlns="http://www.w3.org/2000/svg" width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round">
        <line x1="12" y1="19" x2="12" y2="5"></line>
        <polyline points="5 12 12 5 19 12"></polyline>
      </svg>
    </button>
  </div>
</footer>
