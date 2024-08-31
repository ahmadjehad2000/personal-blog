<script lang="ts">
    import { onMount } from 'svelte';
    import * as config from "$lib/config";
    import { browser } from '$app/environment';

    let isDarkMode = false;
    let isMenuOpen = false;

    function toggleDarkMode() {
        isDarkMode = !isDarkMode;
        document.documentElement.classList.toggle('dark');
    }

    function toggleMenu() {
        isMenuOpen = !isMenuOpen;
    }

    onMount(async () => {
        if (browser) {
            const gsap = (await import('gsap')).default;
            const ScrollTrigger = (await import('gsap/ScrollTrigger')).default;

            gsap.registerPlugin(ScrollTrigger);

            // Floating animation for header
            gsap.to("header", {
                y: 7,
                duration: 3,
                repeat: -1,
                yoyo: true,
                ease: "power1.inOut"
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

            // RGB animation for title, dividers, and nav items
            gsap.to([".title", ".divider", ".nav-item a"], {
                color: "rgb(255,100,100)",
                duration: 2,
                repeat: -1,
                yoyo: true,
                ease: "power1.inOut",
            });

            gsap.to([".title", ".divider", ".nav-item a"], {
                color: "rgb(100,255,100)",
                duration: 2,
                delay: 1,
                repeat: -1,
                yoyo: true,
                ease: "power1.inOut",
            });

            gsap.to([".title", ".divider", ".nav-item a"], {
                color: "rgb(100,100,255)",
                duration: 2,
                delay: 2,
                repeat: -1,
                yoyo: true,
                ease: "power1.inOut",
            });
        }
    });
</script>

<header class="fixed top-4 left-0 right-0 z-50 transition-all duration-300">
    <div class="max-w-3xl mx-auto px-4 sm:px-6 lg:px-8">
        <nav class="flex items-center justify-between bg-white dark:bg-gray-800 shadow-lg rounded-full py-2 px-4 sm:px-6">
            <!-- Centered title with dividers -->
            <div class="flex items-center space-x-2 sm:space-x-4">
                <svg class="w-8 sm:w-10 h-4" viewBox="0 0 100 2" preserveAspectRatio="none">
                    <line x1="0" y1="1" x2="100" y2="1" stroke="currentColor" stroke-width="0.5" class="divider" vector-effect="non-scaling-stroke" />
                </svg>
                <h1 class="title vt323-regular text-lg sm:text-xl md:text-2xl whitespace-nowrap"><a href="/">The Handy Codex</a></h1>
                <svg class="w-12 sm:w-24 h-4" viewBox="0 0 100 2" preserveAspectRatio="none">
                    <line x1="0" y1="1" x2="100" y2="1" stroke="currentColor" stroke-width="0.5" class="divider" vector-effect="non-scaling-stroke" />
                </svg>
            </div>

            <!-- Nav for larger screens -->
            <ul class="hidden lg:flex items-center space-x-4 vt323-regular mr-12">
                <li class="nav-item">
                    <a href="/about" class="text-xs sm:text-2xl hover:text-gray-500 dark:hover:text-gray-400 hover:underline transition-all duration-200">
                        Projects
                    </a>
                </li>
                <li class="nav-item">
                    <a href="/contact" class="text-xs sm:text-2xl hover:text-gray-500 dark:hover:text-gray-400 hover:underline transition-all duration-200">
                        About
                    </a>
                </li>
                <li class="nav-item">
                    <a href="/rss.xml" target="_blank" class="text-xs sm:text-2xl hover:text-gray-500 dark:hover:text-gray-400 hover:underline transition-all duration-200">
                        Blog
                    </a>
                </li>
            </ul>

            <div class="flex items-center space-x-2">
                <button
                    on:click={toggleMenu}
                    class="lg:hidden p-1.5 rounded-md text-gray-600 dark:text-gray-300 hover:text-blue-600 dark:hover:text-blue-400 focus:outline-none"
                    aria-label="Toggle menu"
                >
                    <svg class="h-4 w-4 sm:h-5 sm:w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
                    </svg>
                </button>
                <button
                    on:click={toggleDarkMode}
                    class="p-1.5 rounded-full transition-all duration-300 focus:outline-none bg-gray-200 dark:bg-gray-700 hover:bg-gray-300 dark:hover:bg-gray-600"
                    aria-label={isDarkMode ? 'Switch to light mode' : 'Switch to dark mode'}
                >
                    {#if isDarkMode}
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 sm:h-5 sm:w-5 text-yellow-500" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 3v1m0 16v1m9-9h-1M4 12H3m15.364 6.364l-.707-.707M6.343 6.343l-.707-.707m12.728 0l-.707.707M6.343 17.657l-.707.707M16 12a4 4 0 11-8 0 4 4 0 018 0z" />
                        </svg>
                    {:else}
                        <svg xmlns="http://www.w3.org/2000/svg" class="h-4 w-4 sm:h-5 sm:w-5 text-gray-600" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M20.354 15.354A9 9 0 018.646 3.646 9.003 9.003 0 0012 21a9.003 9.003 0 008.354-5.646z" />
                        </svg>
                    {/if}
                </button>
            </div>
        </nav>
    </div>
</header>
<!-- Mobile menu -->
{#if isMenuOpen}
<div class="fixed inset-0 z-50 bg-white dark:bg-gray-800 lg:hidden">
    <div class="p-4 flex flex-col items-center justify-center h-full">
        <button
            on:click={toggleMenu}
            class="absolute top-4 right-4 p-2 rounded-md text-gray-600 dark:text-gray-300 hover:text-blue-600 dark:hover:text-blue-400 focus:outline-none"
            aria-label="Close menu"
        >
            <svg class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
            </svg>
        </button>
        <ul class="space-y-4 text-center">
            <li>
                <a href="/about" class="vt323-regular text-lg text-gray-600 dark:text-gray-300 hover:text-gray-500 dark:hover:text-gray-400 hover:underline transition-all duration-200">
                    About
                </a>
            </li>
            <li>
                <a href="/contact" class="vt323-regular text-lg text-gray-600 dark:text-gray-300 hover:text-gray-500 dark:hover:text-gray-400 hover:underline transition-all duration-200">
                    Contact
                </a>
            </li>
            <li>
                <a href="/rss.xml" target="_blank" class="vt323-regular text-lg text-gray-600 dark:text-gray-300 hover:text-gray-500 dark:hover:text-gray-400 hover:underline transition-all duration-200">
                    RSS
                </a>
            </li>
        </ul>
    </div>
</div>
{/if}

<style>
    @import url('https://fonts.googleapis.com/css2?family=VT323&display=swap');

    .vt323-regular {
        font-family: "VT323", monospace;
        font-weight: 400;
        font-style: normal;
    }

    :global(body) {
        padding-top: 5rem;
    }
</style>