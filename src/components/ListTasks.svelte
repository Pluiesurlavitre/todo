<script>
    import Task from './Task.svelte'

    export let tasks
    export let categories

    const getCategory = id => ( categories.filter(c => c.id === id)[0] )
</script>

<ul>
    {#each tasks as task}
        <li>
            <Task name={task.name} id={task.id} category={getCategory(task.category_id)} on:deleted/>
        </li>
    {/each}
</ul>