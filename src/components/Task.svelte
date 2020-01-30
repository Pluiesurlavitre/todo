<script>
    import { createEventDispatcher } from 'svelte'

    const dispatch = createEventDispatcher()

    export let id
    export let name
    export let category

    const deleteTask = () => dispatch('deleted', { id: id })

</script>

<div class="border my-2 p-2">
    <div>{name}</div>
    {#if category !== undefined }
    <div>
        Category: { category.name }
    </div>
    {/if}
    <div>
        <button on:click={deleteTask} class="py-1 px-2">Delete Todo</button>
    </div>

</div>