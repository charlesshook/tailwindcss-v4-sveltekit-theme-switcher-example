<script lang="ts">
	import { onMount } from 'svelte';

	let darkMode = false;

	function setTheme(theme: 'light' | 'dark' | 'system') {
		if (theme === 'system') {
			localStorage.removeItem('theme');
		} else {
			localStorage.setItem('theme', theme);
		}

		document.documentElement.classList.toggle(
			'dark',
			localStorage.getItem('theme') === 'dark' ||
				(!localStorage.getItem('theme') &&
					window.matchMedia('(prefers-color-scheme: dark)').matches)
		);

		darkMode = document.documentElement.classList.contains('dark');
	}

	onMount(() => {
		setTheme((localStorage.getItem('theme') as 'light' | 'dark' | 'system') || 'system');
	});
</script>

<div class="mx-auto max-w-lg p-6 text-center">
	<div class="mt-6 flex flex-col gap-2">
		<button
			on:click={() => setTheme('dark')}
			class="rounded-lg bg-gray-300 px-4 py-2 text-gray-800 hover:bg-gray-400 dark:bg-gray-700 dark:text-gray-200 dark:hover:bg-gray-600"
		>
			Enable Dark Mode
		</button>
		<button
			on:click={() => setTheme('light')}
			class="rounded-lg bg-gray-300 px-4 py-2 text-gray-800 hover:bg-gray-400 dark:bg-gray-700 dark:text-gray-200 dark:hover:bg-gray-600"
		>
			Enable Light Mode
		</button>
		<button
			on:click={() => setTheme('system')}
			class="rounded-lg bg-gray-300 px-4 py-2 text-gray-800 hover:bg-gray-400 dark:bg-gray-700 dark:text-gray-200 dark:hover:bg-gray-600"
		>
			Enable System Mode
		</button>
	</div>
</div>
