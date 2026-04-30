<script lang="ts">
  import { onMount } from "svelte";
  import { slide } from "svelte/transition";

  export let currentPath = "/";

  let theme: "light" | "dark" = "light";
  let isMenuOpen = false;
  let currentLang = "en";

  $: currentLang = currentPath.startsWith("/id") ? "id" : "en";

  onMount(() => {
    theme = document.documentElement.classList.contains("dark")
      ? "dark"
      : "light";
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
</script>

<header class="sticky top-0 z-50 glass transition-colors duration-500">
  <nav
    class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8 relative h-14 flex items-center justify-between"
  >
    <!-- Mobile Hamburger (Left) -->
    <div class="sm:hidden flex items-center">
      <button
        on:click={toggleMenu}
        class="p-2 -ml-2 rounded-full hover:bg-black/5 dark:hover:bg-white/10 transition-colors focus:outline-none"
        aria-label="Toggle menu"
      >
        <svg
          xmlns="http://www.w3.org/2000/svg"
          width="20"
          height="20"
          viewBox="0 0 24 24"
          fill="none"
          stroke="currentColor"
          stroke-width="2"
          stroke-linecap="round"
          stroke-linejoin="round"
        >
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
    <div
      class="hidden sm:flex absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2 items-center space-x-10"
    >
      <a
        href={currentLang === "id" ? "/id" : "/"}
        class="text-[14px] font-medium tracking-tight transition-opacity hover:opacity-100 opacity-70"
        >{currentLang === "id" ? "Beranda" : "Home"}</a
      >
      <a
        href={currentLang === "id" ? "/id/blog" : "/blog"}
        class="text-[14px] font-medium tracking-tight transition-opacity hover:opacity-100 opacity-70"
        >Logcat</a
      >
    </div>

    <!-- Right Actions: Language & Theme -->
    <div class="flex items-center space-x-2 ml-auto">
      <!-- Language Switcher -->
      <div
        class="flex items-center bg-black/10 dark:bg-white/5 rounded-full p-1 mr-2"
      >
        <a
          href={getLanguageUrl("id")}
          class="px-2 py-1 rounded-full text-[10px] font-bold transition-all {currentLang ===
          'id'
            ? 'bg-white text-black dark:bg-gray-800 dark:text-white shadow-sm opacity-100'
            : 'opacity-40 hover:opacity-70'}"
        >
          ID
        </a>
        <a
          href={getLanguageUrl("en")}
          class="px-2 py-1 rounded-full text-[10px] font-bold transition-all {currentLang ===
          'en'
            ? 'bg-white text-black dark:bg-gray-800 dark:text-white shadow-sm opacity-100'
            : 'opacity-40 hover:opacity-70'}"
        >
          EN
        </a>
      </div>

      <button
        on:click={toggleTheme}
        class="p-2 rounded-full hover:bg-black/5 dark:hover:bg-white/10 transition-colors focus:outline-none"
        aria-label="Toggle dark mode"
      >
        {#if theme === "light"}
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="18"
            height="18"
            viewBox="0 0 24 24"
            fill="none"
            stroke="currentColor"
            stroke-width="2"
            stroke-linecap="round"
            stroke-linejoin="round"
          >
            <path d="M21 12.79A9 9 0 1 1 11.21 3 7 7 0 0 0 21 12.79z"></path>
          </svg>
        {:else}
          <svg
            xmlns="http://www.w3.org/2000/svg"
            width="18"
            height="18"
            viewBox="0 0 24 24"
            fill="none"
            stroke="currentColor"
            stroke-width="2"
            stroke-linecap="round"
            stroke-linejoin="round"
          >
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
  </nav>

  <!-- Mobile Menu -->
  {#if isMenuOpen}
    <div
      transition:slide={{ duration: 300 }}
      class="sm:hidden glass border-t border-black/5 dark:border-white/5 overflow-hidden"
    >
      <div class="px-4 pt-2 pb-6 space-y-1">
        <a
          href={currentLang === "id" ? "/id" : "/"}
          class="block px-3 py-3 rounded-xl text-base font-medium hover:bg-black/5 dark:hover:bg-white/5 transition-colors"
          on:click={() => (isMenuOpen = false)}
        >
          {currentLang === "id" ? "Beranda" : "Home"}
        </a>
        <a
          href={currentLang === "id" ? "/id/blog" : "/blog"}
          class="block px-3 py-3 rounded-xl text-base font-medium hover:bg-black/5 dark:hover:bg-white/5 transition-colors"
          on:click={() => (isMenuOpen = false)}
        >
          Logcat
        </a>
      </div>
    </div>
  {/if}
</header>
