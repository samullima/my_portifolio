<svelte:head>
    <title>My page</title>
</svelte:head>

<script>
    import projects from "$lib/projects.json";
    import Project from "$lib/Project.svelte";

    import { onMount } from "svelte";

    let githubData = null;
    let loading = true;
    let error = null;

    onMount(async () => {
        try {
            const response = await fetch("https://api.github.com/users/Mike-Kowalski");
            githubData = await response.json();
        } catch (err) {
            error = err;
        }
        loading = false;
    });

    </script>

<h1> Samuel Lima</h1>
   
<img src="images/Thorkell.png" alt="" width="500px">
    
<p>
    Essa imagem mostra o Thorkell, um dos vikings mais fortes de Vinland Saga. <br>
    Este é simplesmente um dos animes que eu mais gosto, pois tem uma história incrível!
</p>

<h2>Latest projects</h2>
<div class="projects">
{#each projects.slice(0, 3) as p}
    <Project data={p} hLevel="3" />
{/each}

{#if loading}
    <p>Loading...</p>
{:else if error}
    <p class="error">Something went wrong: {error.message}</p>
{:else}
    <section>
        <h2>My GitHub Stats</h2>
        <dl>
            <dt>Followers</dt>
            <dd>{githubData.followers}</dd>
            <dt>Following</dt>
            <dd>{githubData.following}</dd>
            <dt>Public Repositories</dt>
            <dd>{githubData.public_repos}</dd>
        </dl>
    </section>
{/if}



</div>

    