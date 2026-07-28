<script lang="ts">
  import { onMount } from "svelte";
  import { List, X, Moon, Sun } from "phosphor-svelte";

  export let currentPath = "/";

  let theme: "light" | "dark" = "dark";
  let isMenuOpen = false;
  let currentLang = "en";
  let scrolled = false;

  $: currentLang = currentPath.startsWith("/id") ? "id" : "en";

  onMount(() => {
    const savedTheme = localStorage.getItem("theme");
    if (savedTheme === "dark" || savedTheme === "light") {
      theme = savedTheme;
    } else if (typeof window !== "undefined") {
      theme = document.documentElement.classList.contains("dark") || window.matchMedia("(prefers-color-scheme: dark)").matches ? "dark" : "light";
    }
    
    if (theme === "dark") {
      document.documentElement.classList.add("dark");
    } else {
      document.documentElement.classList.remove("dark");
    }

    const onScroll = () => {
      scrolled = window.scrollY > 20;
    };
    window.addEventListener("scroll", onScroll, { passive: true });
    onScroll();
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

<div class="fixed top-0 left-0 right-0 z-50 flex flex-col items-center p-3 sm:p-6 pointer-events-none">
  <!-- Top Header Pill Bar -->
  <header class="pointer-events-auto w-full max-w-5xl relative z-20 glass rounded-full px-5 py-3 shadow-lg border border-[var(--border)] transition-all duration-300 ease-out flex items-center justify-between">
    
    <!-- Left: Monogram Logo -->
    <div class="flex items-center">
      <a href={currentLang === "id" ? "/id" : "/"} class="font-mono text-lg font-bold tracking-tight px-3 py-1.5 rounded-lg hover:bg-[var(--accent-glow)] transition-colors text-[var(--text)]">
        [C9]
      </a>
    </div>

    <!-- Centered Links (Desktop) -->
    <nav class="hidden sm:flex items-center space-x-1 absolute left-1/2 -translate-x-1/2">
      <a href={currentLang === "id" ? "/id" : "/"} class="px-4 py-2 text-sm font-medium rounded-full transition-colors hover:text-[var(--text)] hover:bg-[var(--accent-glow)] {isActive(currentLang === 'id' ? '/id' : '/', true) ? 'text-[var(--text)] bg-[var(--accent-glow)]' : 'text-[var(--subtle)]'}">
        {currentLang === "id" ? "Beranda" : "Home"}
      </a>
      <a href={currentLang === "id" ? "/id/projects" : "/projects"} class="px-4 py-2 text-sm font-medium rounded-full transition-colors hover:text-[var(--text)] hover:bg-[var(--accent-glow)] {isActive(currentLang === 'id' ? '/id/projects' : '/projects') ? 'text-[var(--text)] bg-[var(--accent-glow)]' : 'text-[var(--subtle)]'}">
        {currentLang === "id" ? "Proyek" : "Projects"}
      </a>
      <a href={currentLang === "id" ? "/id/blog" : "/blog"} class="px-4 py-2 text-sm font-medium rounded-full transition-colors hover:text-[var(--text)] hover:bg-[var(--accent-glow)] {isActive(currentLang === 'id' ? '/id/blog' : '/blog') ? 'text-[var(--text)] bg-[var(--accent-glow)]' : 'text-[var(--subtle)]'}">
        Logcat
      </a>
    </nav>

    <!-- Right Actions: Language, Theme & Mobile Menu -->
    <div class="flex items-center space-x-2 sm:space-x-3">
      <!-- Language Switcher (Desktop) -->
      <div class="hidden sm:flex items-center bg-[var(--bg)] border border-[var(--border)] rounded-full p-1 shadow-sm">
        <a href={getLanguageUrl("id")} class="flex items-center justify-center min-w-[36px] min-h-[28px] px-2 rounded-full text-xs font-bold font-mono transition-all {currentLang === 'id' ? 'bg-[var(--text)] text-[var(--bg)]' : 'text-[var(--subtle)] hover:text-[var(--text)]'}">ID</a>
        <a href={getLanguageUrl("en")} class="flex items-center justify-center min-w-[36px] min-h-[28px] px-2 rounded-full text-xs font-bold font-mono transition-all {currentLang === 'en' ? 'bg-[var(--text)] text-[var(--bg)]' : 'text-[var(--subtle)] hover:text-[var(--text)]'}">EN</a>
      </div>

      <!-- Theme Toggle -->
      <button on:click={toggleTheme} class="p-2 rounded-full hover:bg-[var(--accent-glow)] text-[var(--subtle)] hover:text-[var(--accent)] transition-all focus:outline-none focus:ring-2 focus:ring-[var(--accent)] relative" aria-label="Toggle dark mode">
        {#if theme === "light"}
          <Moon size={20} weight="bold" />
        {:else}
          <Sun size={20} weight="bold" />
        {/if}
      </button>

      <!-- Mobile Hamburger -->
      <button on:click={toggleMenu} class="sm:hidden p-2 rounded-full hover:bg-[var(--accent-glow)] text-[var(--text)] transition-colors focus:outline-none" aria-label="Toggle menu">
        {#if isMenuOpen}
          <X size={22} weight="bold" />
        {:else}
          <List size={22} weight="bold" />
        {/if}
      </button>
    </div>
  </header>

  <!-- Mobile Dropdown Menu -->
  {#if isMenuOpen}
    <div class="pointer-events-auto w-full max-w-5xl mt-2 sm:hidden glass rounded-2xl p-4 shadow-2xl border border-[var(--border)] bg-[var(--bg)]/95 backdrop-blur-xl relative z-10 transition-all">
      <div class="space-y-1">
        <a
          href={currentLang === "id" ? "/id" : "/"}
          class="block px-4 py-3 rounded-xl text-sm font-semibold transition-colors {isActive(currentLang === 'id' ? '/id' : '/', true) ? 'bg-[var(--accent-glow)] text-[var(--accent)]' : 'text-[var(--text)] hover:bg-black/5 dark:hover:bg-white/5'}"
          on:click={() => (isMenuOpen = false)}
        >
          {currentLang === "id" ? "Beranda" : "Home"}
        </a>
        <a
          href={currentLang === "id" ? "/id/projects" : "/projects"}
          class="block px-4 py-3 rounded-xl text-sm font-semibold transition-colors {isActive(currentLang === 'id' ? '/id/projects' : '/projects') ? 'bg-[var(--accent-glow)] text-[var(--accent)]' : 'text-[var(--text)] hover:bg-black/5 dark:hover:bg-white/5'}"
          on:click={() => (isMenuOpen = false)}
        >
          {currentLang === "id" ? "Proyek" : "Projects"}
        </a>
        <a
          href={currentLang === "id" ? "/id/blog" : "/blog"}
          class="block px-4 py-3 rounded-xl text-sm font-semibold transition-colors {isActive(currentLang === 'id' ? '/id/blog' : '/blog') ? 'bg-[var(--accent-glow)] text-[var(--accent)]' : 'text-[var(--subtle)] hover:bg-black/5 dark:hover:bg-white/5'}"
          on:click={() => (isMenuOpen = false)}
        >
          Logcat
        </a>
        
        <div class="h-px w-full bg-[var(--border)] my-2"></div>
        
        <!-- Mobile Language Switch -->
        <div class="flex items-center justify-between px-4 py-2">
          <span class="text-xs font-mono text-[var(--subtle)] uppercase tracking-wider font-semibold">Language</span>
          <div class="flex items-center bg-[var(--bg)] border border-[var(--border)] rounded-full p-1">
            <a href={getLanguageUrl("id")} class="flex items-center justify-center min-w-[36px] px-3 py-1.5 rounded-full text-xs font-bold font-mono transition-all {currentLang === 'id' ? 'bg-[var(--text)] text-[var(--bg)]' : 'text-[var(--subtle)] hover:text-[var(--text)]'}">ID</a>
            <a href={getLanguageUrl("en")} class="flex items-center justify-center min-w-[36px] px-3 py-1.5 rounded-full text-xs font-bold font-mono transition-all {currentLang === 'en' ? 'bg-[var(--text)] text-[var(--bg)]' : 'text-[var(--subtle)] hover:text-[var(--text)]'}">EN</a>
          </div>
        </div>
      </div>
    </div>
  {/if}
</div>
