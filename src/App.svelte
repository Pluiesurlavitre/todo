<script>
    import Tailwindcss from './Tailwindcss.svelte'
    import { writable } from 'svelte/store'

    const store = writable(localStorage.getItem('store') || '')
    import CreateTask from './components/CreateTask.svelte'
    import ListTasks from './components/ListTasks.svelte'

    function uuidv4 () {
        return 'xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx'.replace(/[xy]/g, function (c) {
            var r = Math.random() * 16 | 0, v = c == 'x' ? r : (r & 0x3 | 0x8)
            return v.toString(16)
        })
    }

    store.subscribe(val => localStorage.setItem('store', val))

    const storeItems = writable(JSON.parse(localStorage.getItem('items')) || [])

    storeItems.subscribe(val => localStorage.setItem('items', JSON.stringify(val)))

    let item = ''

    function handleClick () {
        storeItems.update(n => [...n, { 'name': item, id: uuidv4() }])
        item = ''
    }

    function handleDelete (e) {
        console.log('here')
        storeItems.update(n => [...n].filter(i => i.id !== e.detail.id))
    }

    function handleCreated (e) {
        storeItems.update(n => [...n, { 'name': e.detail, id: uuidv4() }])
        item = ''
    }

</script>

<main class="container mx-auto">

    <CreateTask on:created={handleCreated}/>

    <ListTasks tasks={$storeItems} on:message={handleDelete}/>

</main>

<style>


</style>

