<script lang="ts">
    import { onMount } from 'svelte'

    //  Imports

    //  Props
    export let id: number
    export let title: string
    export let body: string

    //  Methods Declarations
    const trimContent = (content: string, length: number = 50) => {
        if (content.length > length) {
            return `${content.substring(0, length)}...`
        }
        return content
    }

    // Logic
    const fetchImage = (async () => {
        const response = await fetch('https://dog.ceo/api/breeds/image/random')
        return await response.json()
    })()
</script>

<article class="bg-white border rounded-lg shadow p-4 hover:shadow-xl">
    <span class="text-sm">{id}</span>
    <h2 class="text-xl">{trimContent(title, 20)}</h2>
    <p class="my-3">{trimContent(body)}</p>
    {#await fetchImage}
        <p>...loading</p>
    {:then data}
        <img class="w-56" src={data.message} alt="Dog image" />
    {:catch error}
        <p>An error occurred!</p>
    {/await}
</article>
