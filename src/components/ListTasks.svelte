<script>
    import Task from './Task.svelte'

    export let tasks
</script>

<ul>
    {#each tasks as task}
        <li>
            <Task {...task} on:message/>
        </li>
    {/each}
</ul>