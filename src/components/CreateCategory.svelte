<script>
    import { createEventDispatcher } from 'svelte'

    const dispatch = createEventDispatcher()

    let title = ''

    function handleSubmit () {
        dispatch('created', title)
        title = ''
    }

</script>

<form on:submit|preventDefault={handleSubmit}>

    <input type="text" bind:value={title} placeholder="add a category">
    <button type="submit">Add</button>

</form>
