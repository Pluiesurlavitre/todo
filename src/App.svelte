<script>
    import Tailwindcss from './Tailwindcss.svelte'
    import { writable } from 'svelte/store'

    const store = writable(localStorage.getItem('store') || '')
    import CreateTask from './components/CreateTask.svelte'
    import ListTasks from './components/ListTasks.svelte'
    import CreateCategory from './components/CreateCategory.svelte'
    import ListCategories from './components/ListCategories.svelte'

    function uuidv4 () {
        return 'xxxxxxxx-xxxx-4xxx-yxxx-xxxxxxxxxxxx'.replace(/[xy]/g, function (c) {
            var r = Math.random() * 16 | 0, v = c == 'x' ? r : (r & 0x3 | 0x8)
            return v.toString(16)
        })
    }

    const tasks = writable(JSON.parse(localStorage.getItem('tasks')) || [])
    tasks.subscribe(val => localStorage.setItem('tasks', JSON.stringify(val)))

    const categories = writable(JSON.parse(localStorage.getItem('categories')) || [])
    categories.subscribe(v => localStorage.setItem('categories', JSON.stringify(v)))

    const handleCreateTask = e => tasks.update(n => [...n, { 'name': e.detail.title, id: uuidv4(), category_id: e.detail.selected }])
    const handleCreateCategory = e => categories.update(n => [...n, { 'name': e.detail, id: uuidv4() }])
    const handleDeleteTask = e => tasks.update(n => [...n].filter(i => i.id !== e.detail.id))

</script>

<main class="container mx-auto">

    <CreateTask on:created={handleCreateTask} categories={$categories}/>

    <ListTasks tasks={$tasks} categories={$categories} on:deleted={handleDeleteTask}/>

    <CreateCategory on:created={handleCreateCategory}/>

    <ListCategories categories={$categories}/>


</main>

<style>


</style>

