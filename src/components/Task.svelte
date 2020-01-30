<script>
    import { createEventDispatcher } from 'svelte'
    const dispatch = createEventDispatcher()

    export let id
    export let name

    function deleteTask () {
        dispatch('message', {id: id})
    }


</script>

<p>
    {name} - <button on:click={deleteTask}>Delete</button>
</p>