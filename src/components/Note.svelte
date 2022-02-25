<script lang="ts">
    //  Imports
    import { createEventDispatcher } from 'svelte'
    import { formatDate } from '../libs/utils'

    //  Props
    export let id: number
    export let title: string
    export let content: string
    export let date: string
    export let isFavorite: boolean
    export let tags: string[]

    //  Methods Declarations
    const dispatch = createEventDispatcher()
    const trimContent = (content: string) => {
        if (content.length > 100) {
            return `${content.substring(0, 100)}...`
        }
        return content
    }
</script>

<div class="relative bg-white border rounded-lg shadow p-4 hover:shadow-xl" on:click>
    <h2 class="text-xl">{title}</h2>
    <p class="my-3">{trimContent(content)}</p>

    <div class="flex">
        {#each tags as tag (tag)}
            <span class="bg-zinc-200 rounded-full px-3 mr-1">{tag}</span>
        {/each}
    </div>

	<div class="absolute top-1 right-2" on:click|stopPropagation={() => dispatch('toggleFavorite', id)}>
		<span class={'text-xl ' + (isFavorite ? 'text-yellow-400' : 'text-zinc-300')}>
			<i class="bi bi-star-fill" />
		</span>
	</div>
    <p class="text-zinc-600">{formatDate(date)}</p>
</div>
