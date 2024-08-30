<script lang="ts">
  const currentYear = new Date().getFullYear();
</script>

<footer class="bg-white dark:bg-gray-800 shadow-lg mt-auto">
  <div class="max-w-6xl mx-auto px-4 py-6 sm:px-6 lg:px-8">
    <div class="flex flex-col md:flex-row justify-between items-center space-y-4 md:space-y-0">
      <!-- Logo and tagline -->
      <div class="flex flex-col items-center md:items-start font-mono">
        <div class="text-xl font-semibold text-gray-800 dark:text-white">
          The Handy Codex
        </div>
        <p class="text-sm text-gray-600 dark:text-gray-300 mt-1">
          This website was made with 
          <a 
            class="text-orange-500 hover:underline" 
            href="https://kit.svelte.dev/" 
            target="_blank" 
            rel="noopener noreferrer"
          >
            SvelteKit
          </a> 
          proudly!
        </p>
      </div>

      <!-- Social icons (GitHub and LinkedIn) -->
      <div class="flex space-x-4 font-mono">
        <a 
          href="https://www.linkedin.com/in/ahmadjehad2000/" 
          target="_blank" 
          rel="noopener noreferrer" 
          class="text-gray-400 hover:text-blue-500 dark:hover:text-blue-400 transition-colors duration-200"
          aria-label="LinkedIn Profile"
        >
          <svg class="h-6 w-6" fill="currentColor" viewBox="0 0 24 24" aria-hidden="true">
            <path d="M20.447 20.452h-3.554v-5.569c0-1.328-.027-3.037-1.852-3.037-1.853 0-2.136 1.445-2.136 2.939v5.667H9.351V9h3.414v1.561h.046c.477-.9 1.637-1.85 3.37-1.85 3.601 0 4.267 2.37 4.267 5.455v6.286zM5.337 7.433c-1.144 0-2.063-.926-2.063-2.065 0-1.138.92-2.063 2.063-2.063 1.14 0 2.064.925 2.064 2.063 0 1.139-.925 2.065-2.064 2.065zm1.782 13.019H3.555V9h3.564v11.452zM22.225 0H1.771C.792 0 0 .774 0 1.729v20.542C0 23.227.792 24 1.771 24h20.451C23.2 24 24 23.227 24 22.271V1.729C24 .774 23.2 0 22.222 0h.003z"/>
          </svg>
        </a>
        <a 
          href="https://github.com/ahmadjehad2000" 
          target="_blank" 
          rel="noopener noreferrer" 
          class="text-gray-400 hover:text-blue-500 dark:hover:text-blue-400 transition-colors duration-200"
          aria-label="GitHub Profile"
        >
          <svg class="h-6 w-6" fill="currentColor" viewBox="0 0 24 24" aria-hidden="true">
            <path fill-rule="evenodd" d="M12 2C6.477 2 2 6.484 2 12.017c0 4.425 2.865 8.18 6.839 9.504.5.092.682-.217.682-.483 0-.237-.008-.868-.013-1.703-2.782.605-3.369-1.343-3.369-1.343-.454-1.158-1.11-1.466-1.11-1.466-.908-.62.069-.608.069-.608 1.003.07 1.531 1.032 1.531 1.032.892 1.53 2.341 1.088 2.91.832.092-.647.35-1.088.636-1.338-2.22-.253-4.555-1.113-4.555-4.951 0-1.093.39-1.988 1.029-2.688-.103-.253-.446-1.272.098-2.65 0 0 .84-.27 2.75 1.026A9.564 9.564 0 0112 6.844c.85.004 1.705.115 2.504.337 1.909-1.296 2.747-1.027 2.747-1.027.546 1.379.202 2.398.1 2.651.64.7 1.028 1.595 1.028 2.688 0 3.848-2.339 4.695-4.566 4.943.359.309.678.92.678 1.855 0 1.338-.012 2.419-.012 2.747 0 .268.18.58.688.482A10.019 10.019 0 0022 12.017C22 6.484 17.522 2 12 2z" clip-rule="evenodd" />
          </svg>
        </a>
      </div>
    </div>

    <!-- Copyright -->
    <div class="font-mono mt-6 border-t border-gray-200 dark:border-gray-700 pt-4 text-center text-sm text-gray-500 dark:text-gray-400">
      © {currentYear} By Ahmad Jehad. All rights reserved.
    </div>
  </div>
</footer>