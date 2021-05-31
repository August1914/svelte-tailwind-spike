<script>
	import Tailwindcss from './Tailwindcss.svelte';
	import Search from './Search.svelte'
	export let name;

	let usernameInputField = '';
	let repositories = undefined;

	async function onSubmit() {
		const url = `https://api.github.com/users/${usernameInputField}/repos`;

		const response = await fetch(url);
		repositories = await response.json();
		console.log('loaded repositories', repositories)
	}
</script>

<Tailwindcss />
<nav class="text-white shadow-lg">
	<div class="container mx-auto">
		<div class="flex">
			<a href="#" class="text-white text-3xl font-bold p-3">APP LOGO</a>
			<div class="ml-55 mt-4">
				<ul class="text-white sm:self-center text-xl">
					<li class="sm:inline-block">
						<a href="#" class="p-3 hover:text-red-900">About</a>
					</li>
					<li class="sm:inline-block">
						<a href="#" class="p-3 hover:text-red-900">Services</a>
					</li>
					<li class="sm:inline-block">
						<a href="#" class="p-3 hover:text-red-900">Blog</a>
					</li>
					<li class="sm:inline-block">
						<a href="#" class="p-3 hover:text-red-900">Contact</a>
					</li>
				</ul>
			</div>
		</div>
	</div>
</nav>

<main class="container mx-auto text-center ">
	<h1 class="my-4 text-5xl font-semibold text-indigo-500">Hello {name}!</h1>
	<h2 class="bg-blue-500 text-white">This is a demo of Svelt with Tailwindcss</h2>
	<p>Visit the <a href="https://svelte.dev/tutorial">Svelte tutorial</a> to learn how to build Svelte apps.</p>
	<div>
		<p class="mt-10 text-gray-900">Search and filter public github repositories by git user:</p>
	</div>
    <div class="mt-2">
	<form on:submit|preventDefault={onSubmit}>
		<lable for="username">GitHub username:</lable>
		<input type="text" name="username" placeholder="jackfranklin" bind:value={usernameInputField}/>
		<button type="submit" class="p-2 font-sans text-xs text-blue-500 bg-transparent border border-blue-500 rounded-lg ring-1 hover:bg-blue-500 hover:text-white">Load repositories</button>
	</form>
	{#if repositories}
		<Search {repositories} />
	{/if}
	</div>
</main>

<style>

</style>
