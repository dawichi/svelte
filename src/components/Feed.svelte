<script lang="ts">
    interface Post {
        userId: number
        id: number
        title: string
        body: string
    }

    import { onMount } from 'svelte'
    import { apiData, posts } from '../utils/posts'
    import Post from './Post.svelte'

    onMount(async () => {
        try {
            const response = await fetch('https://jsonplaceholder.typicode.com/posts')
            const data = await response.json()
            apiData.set(data)
        } catch (error) {
            console.log(error)
            return []
        }
    })
</script>

<div class="container mx-auto p-4 rounded bg-zinc-200">
    <div class="grid gap-4 grid-cols-1 md:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4">
        {#each $posts as post}
            <Post id={post.id} title={post.title} body={post.body} />
        {/each}
    </div>
</div>
