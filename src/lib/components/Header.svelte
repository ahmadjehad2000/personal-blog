<script lang="ts">
    import { onMount } from 'svelte';
    import * as config from "$lib/config";
    import dark from "../../../static/assets/dark.png";
    import light from "../../../static/assets/light.png";
    import { browser } from '$app/environment';

    let isDarkMode = false;

    function toggleDarkMode() {
        isDarkMode = !isDarkMode;
        document.documentElement.classList.toggle('dark');
    }

    onMount(async () => {
        if (browser) {
            const gsap = (await import('gsap')).default;
            const ScrollTrigger = (await import('gsap/ScrollTrigger')).default;

            gsap.registerPlugin(ScrollTrigger);

            // Emoji rolling animation controlled by scroll
            gsap.to(".emoji", {
                rotation: 360,
                ease: "none",
                scrollTrigger: {
                    trigger: "body",
                    start: "top top",
                    end: "bottom bottom",
                    scrub: 1 // Controls the speed of the rotation relative to the scroll speed
                }
            });

            // Scrolling animation for nav items
            gsap.utils.toArray(".nav-item").forEach((item, index) => {
                gsap.from(item, {
                    opacity: 0,
                    y: 20,
                    duration: 0.5,
                    ease: "power2.out",
                    scrollTrigger: {
                        trigger: item,
                        start: "top bottom-=100",
                        toggleActions: "play none none reverse"
                    },
                    delay: index * 0.1
                });
            });

            // Header shrink effect on scroll
            gsap.to("header", {
                scrollTrigger: {
                    trigger: "body",
                    start: "top top",
                    end: "+=200",
                    scrub: true
                },
                height: "3rem",
                padding: "0.5rem",
                ease: "power2.out"
            });
        }
    });
</script>

<header class="fixed top-4 left-0 right-0 z-50 transition-all duration-300">
    <div class="max-w-4xl mx-auto px-4 sm:px-6 lg:px-8">
        <nav class="flex items-center justify-between bg-white dark:bg-gray-800 shadow-lg rounded-full py-2 px-4 sm:px-6">
            <!-- Title and Emoji Container -->
            <div class="title-container flex items-center space-x-2 text-base font-mono flex-shrink-0 group relative">
                <div class="emoji text-xl sm:text-2xl" aria-hidden="true">⚙️</div>
                <a href="/" class="text-sm sm:text-base font-semibold text-gray-800 dark:text-white hover:text-blue-600 dark:hover:text-blue-400 transition-colors duration-200">
                    {config.title}
                </a>
                <div class="emoji text-xl sm:text-2xl" aria-hidden="true">⚙️</div>
                <span class="tooltip">Home</span>
            </div>

            <!-- Nav -->
            <ul class="hidden sm:flex items-center space-x-1 sm:space-x-2 font-mono mr-16">
                <li class="group relative px-2 py-1 nav-item">
                    <a href="/about" class="text-xs sm:text-sm text-gray-600 dark:text-gray-300 hover:text-blue-600 dark:hover:text-blue-400 transition-all duration-200 uppercase tracking-wider font-medium border-b-2 border-transparent hover:border-blue-600 dark:hover:border-blue-400 pb-1">
                        About
                    </a>
                    <span class="tooltip">About</span>
                </li>
                <li class="group relative px-2 py-1 nav-item">
                    <a href="/contact" class="text-xs sm:text-sm text-gray-600 dark:text-gray-300 hover:text-blue-600 dark:hover:text-blue-400 transition-all duration-200 uppercase tracking-wider font-medium border-b-2 border-transparent hover:border-blue-600 dark:hover:border-blue-400 pb-1">
                        Contact
                    </a>
                    <span class="tooltip">Contact</span>
                </li>
                <li class="group relative px-2 py-1 nav-item">
                    <a href="/rss.xml" target="_blank" class="text-xs sm:text-sm text-gray-600 dark:text-gray-300 hover:text-blue-600 dark:hover:text-blue-400 transition-all duration-200 uppercase tracking-wider font-medium border-b-2 border-transparent hover:border-blue-600 dark:hover:border-blue-400 pb-1">
                        RSS
                    </a>
                    <span class="tooltip">RSS Feed</span>
                </li>
            </ul>

            <!-- Theme Toggle -->
            <div class="relative group flex-shrink-0 ml-2 sm:ml-4">
                <button
                    on:click={toggleDarkMode}
                    class="p-1.5 sm:p-2 rounded-full transition-all duration-300 focus:outline-none hover:scale-110 bg-gray-100 dark:bg-gray-700"
                    aria-label={isDarkMode ? 'Switch to light mode' : 'Switch to dark mode'}
                >
                    {#if isDarkMode}
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 sm:h-5 sm:w-5 text-yellow-400 hover:text-yellow-300 transition-all duration-300" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 3v1m0 16v1m9-9h-1M4 12H3m15.364 6.364l-.707-.707M6.343 6.343l-.707-.707m12.728 0l-.707.707M6.343 17.657l-.707.707M16 12a4 4 0 11-8 0 4 4 0 018 0z" />
                        </svg>
                    {:else}
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 sm:h-5 sm:w-5 text-gray-600 hover:text-gray-800 transition-all duration-300" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M20.354 15.354A9 9 0 018.646 3.646 9.003 9.003 0 0012 21a9.003 9.003 0 008.354-5.646z" />
                        </svg>
                    {/if}
                </button>
                <span class="tooltip">
                    {isDarkMode ? 'Switch to Light mode' : 'Switch to Dark mode'}
                </span>
            </div>
        </nav>
    </div>
</header>

<style>
    .emoji {
        color: rgba(0, 0, 0, 0.7);
    }
    .tooltip {
        @apply absolute hidden bg-gray-800 text-white text-xs px-2 py-1 rounded-md -bottom-8 left-1/2 transform -translate-x-1/2 z-10;
    }
    :global(body) {
        padding-top: 4rem;
    }
</style>
