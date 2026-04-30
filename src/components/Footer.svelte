<script lang="ts">
  const today = new Date();
</script>

<footer class="py-10 text-center text-sm opacity-60">
  <div class="max-w-4xl mx-auto px-4">
    <div class="mt-4 flex justify-center space-x-6">
      <a
        href="https://linkedin.com/in/mtantowij"
        target="_blank"
        class="hover:opacity-70 transition-opacity">LinkedIn</a
      >
      <a
        href="https://wa.me/628115114383"
        target="_blank"
        class="hover:opacity-70 transition-opacity">WhatsApp</a
      >
      <a
        href="mailto:tantowijauhari16@gmail.com"
        class="hover:opacity-70 transition-opacity">Email</a
      >
    </div>
    <br />
    <p>
      &copy; {today.getFullYear()} Muhammad Tantowi Jauhari. All rights reserved.
    </p>
    <p>Powered by Astro & Svelte</p>
  </div>
</footer>
