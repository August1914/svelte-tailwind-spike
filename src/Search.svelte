<script>
    export let repositories;
    let userSearchTerm = "";
    $: filteredRepos = repositories.filter((repo) => {
        return repo.name.toLowerCase().includes(userSearchTerm.toLowerCase())
    });

    function filter(repositories, userSearchTerm) {
        return repositories.filter((repo) => {
            return repo.name.toLowerCase().includes(userSearchTerm.toLowerCase());
        });
    }
    $: console.log(userSearchTerm)
</script>

<style>

  li:nth-child(odd) {
      background-color: lightblue;
  }

</style>

<div>
    <p>Filter the list with this Svelte search component:</p>
    <form class="mb-2">
        <input type="text" bind:value={userSearchTerm} placeholder="search for repositories" class="rounded-md border-2"/>
    </form>

{#each filter(repositories, userSearchTerm) as repository}
<li class="list-none py-2"><strong>{repository.name}</strong><span class="block">{repository.url}</span></li>
{/each}
</div>
