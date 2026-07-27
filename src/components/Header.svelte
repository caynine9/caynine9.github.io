<script lang="ts">
  import { onMount } from "svelte";
  import { slide } from "svelte/transition";

  export let currentPath = "/";

  let theme: "light" | "dark" = "light";
  let isMenuOpen = false;
  let currentLang = "en";
  let scrolled = false;

  $: currentLang = currentPath.startsWith("/id") ? "id" : "en";

  onMount(() => {
    theme = document.documentElement.classList.contains("dark") ? "dark" : "light";

    const onScroll = () => {
      scrolled = window.scrollY > 20;
    };
    window.addEventListener("scroll", onScroll, { passive: true });
    return () => window.removeEventListener("scroll", onScroll);
  });

  function toggleTheme() {
    theme = theme === "light" ? "dark" : "light";
    if (theme === "dark") {
      document.documentElement.classList.add("dark");
    } else {
      document.documentElement.classList.remove("dark");
    }
    localStorage.setItem("theme", theme);
  }

  function toggleMenu() {
    isMenuOpen = !isMenuOpen;
  }

  function getLanguageUrl(lang: string) {
    if (lang === "id") {
      return currentPath.startsWith("/id")
        ? currentPath
        : "/id" + (currentPath === "/" ? "" : currentPath);
    } else {
      return currentPath.startsWith("/id")
        ? currentPath.replace("/id", "") || "/"
        : currentPath;
    }
  }

  function isActive(path: string, exact = false) {
    if (exact) return currentPath === path;
    if (path === "/" || path === "/id") return currentPath === path;
    return currentPath.startsWith(path);
  }
</script>

<div class="fixed top-0 left-0 right-0 z-50 flex justify-center p-4 sm:p-6 pointer-events-none transition-all duration-500 {scrolled ? 'translate-y-0' : 'translate-y-2'}">
  <header class="pointer-events-auto w-full max-w-4xl {scrolled ? 'glass rounded-full px-6 py-3' : 'bg-transparent px-2 py-4'} transition-all duration-500 flex items-center justify-between">
    
    <!-- Mobile Hamburger (Left) -->
    <div class="sm:hidden flex items-center">
      <button on:click={toggleMenu} class="p-2 -ml-2 rounded-full hover:bg-[var(--accent-glow)] transition-colors focus:outline-none" aria-label="Toggle menu">
        <svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
          {#if isMenuOpen}
            <line x1="18" y1="6" x2="6" y2="18"></line>
            <line x1="6" y1="6" x2="18" y2="18"></line>
          {:else}
            <line x1="3" y1="12" x2="21" y2="12"></line>
            <line x1="3" y1="6" x2="21" y2="6"></line>
            <line x1="3" y1="18" x2="21" y2="18"></line>
          {/if}
        </svg>
      </button>
    </div>

    <!-- Centered Links (Desktop) -->
    <div class="hidden sm:flex items-center space-x-2 {scrolled ? '' : 'pl-2'}">
      <a href={currentLang === "id" ? "/id" : "/"} class="relative px-4 py-2 text-sm font-medium transition-colors hover:text-[var(--accent)] {isActive(currentLang === 'id' ? '/id' : '/', true) ? 'text-[var(--accent)]' : 'text-[var(--text)] opacity-70'}">
        {currentLang === "id" ? "Beranda" : "Home"}
        {#if isActive(currentLang === 'id' ? '/id' : '/', true)}
          <span class="absolute bottom-0 left-1/2 -translate-x-1/2 w-4 h-0.5 bg-[var(--accent)] rounded-full"></span>
        {/if}
      </a>
      <a href={currentLang === "id" ? "/id/blog" : "/blog"} class="relative px-4 py-2 text-sm font-medium transition-colors hover:text-[var(--accent)] {isActive(currentLang === 'id' ? '/id/blog' : '/blog') ? 'text-[var(--accent)]' : 'text-[var(--text)] opacity-70'}">
        Logcat
        {#if isActive(currentLang === 'id' ? '/id/blog' : '/blog')}
          <span class="absolute bottom-0 left-1/2 -translate-x-1/2 w-4 h-0.5 bg-[var(--accent)] rounded-full"></span>
        {/if}
      </a>
    </div>

    <!-- Right Actions: Language & Theme -->
    <div class="flex items-center space-x-3 ml-auto">
      <!-- Language Switcher -->
      <div class="flex items-center bg-[rgba(var(--accent-rgb),0.05)] border border-[var(--border)] rounded-full p-1">
        <a href={getLanguageUrl("id")} class="px-2.5 py-1 rounded-full text-[11px] font-bold transition-all {currentLang === 'id' ? 'bg-[var(--accent)] text-white shadow-md shadow-[var(--accent-glow)]' : 'opacity-50 hover:opacity-100'}">ID</a>
        <a href={getLanguageUrl("en")} class="px-2.5 py-1 rounded-full text-[11px] font-bold transition-all {currentLang === 'en' ? 'bg-[var(--accent)] text-white shadow-md shadow-[var(--accent-glow)]' : 'opacity-50 hover:opacity-100'}">EN</a>
      </div>

      <button on:click={toggleTheme} class="p-2 rounded-full hover:bg-[var(--accent-glow)] text-[var(--accent)] transition-all focus:outline-none" aria-label="Toggle dark mode">
        {#if theme === "light"}
          <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round">
            <path d="M21 12.79A9 9 0 1 1 11.21 3 7 7 0 0 0 21 12.79z"></path>
          </svg>
        {:else}
          <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2.5" stroke-linecap="round" stroke-linejoin="round">
            <circle cx="12" cy="12" r="5"></circle>
            <line x1="12" y1="1" x2="12" y2="3"></line>
            <line x1="12" y1="21" x2="12" y2="23"></line>
            <line x1="4.22" y1="4.22" x2="5.64" y2="5.64"></line>
            <line x1="18.36" y1="18.36" x2="19.78" y2="19.78"></line>
            <line x1="1" y1="12" x2="3" y2="12"></line>
            <line x1="21" y1="12" x2="23" y2="12"></line>
            <line x1="4.22" y1="19.78" x2="5.64" y2="18.36"></line>
            <line x1="18.36" y1="5.64" x2="19.78" y2="4.22"></line>
          </svg>
        {/if}
      </button>
    </div>
  </header>
</div>

<!-- Mobile Menu Dropdown -->
{#if isMenuOpen}
  <div transition:slide={{ duration: 300, easing: (t) => 1 - Math.pow(1 - t, 4) }} class="sm:hidden fixed top-[4.5rem] left-4 right-4 z-40 overflow-hidden glass rounded-2xl shadow-2xl">
    <div class="p-2 space-y-1">
      <a
        href={currentLang === "id" ? "/id" : "/"}
        class="block px-4 py-3 rounded-xl text-base font-medium transition-colors {isActive(currentLang === 'id' ? '/id' : '/', true) ? 'bg-[var(--accent-glow)] text-[var(--accent)]' : 'hover:bg-black/5 dark:hover:bg-white/5'}"
        on:click={() => (isMenuOpen = false)}
      >
        {currentLang === "id" ? "Beranda" : "Home"}
      </a>
      <a
        href={currentLang === "id" ? "/id/blog" : "/blog"}
        class="block px-4 py-3 rounded-xl text-base font-medium transition-colors {isActive(currentLang === 'id' ? '/id/blog' : '/blog') ? 'bg-[var(--accent-glow)] text-[var(--accent)]' : 'hover:bg-black/5 dark:hover:bg-white/5'}"
        on:click={() => (isMenuOpen = false)}
      >
        Logcat
      </a>
    </div>
  </div>
{/if}
