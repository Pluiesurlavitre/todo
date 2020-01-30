<script>
    import { createEventDispatcher } from 'svelte'

    const dispatch = createEventDispatcher()

    export let categories

    let title = ''
    let selected

    function handleSubmit () {
        dispatch('created', {title, selected})
        selected = title = ''
    }

</script>

<form on:submit|preventDefault={handleSubmit}>

    <input type="text" bind:value={title} placeholder="add a todo">
    <select bind:value={selected}>
        <option value="">Chose a category</option>

        {#each categories as category }
            <option value={category.id}>{category.name}</option>
        {/each}

    </select>
    <button type="submit">Add</button>

</form>
