<script lang="ts">
    //  Global Imports
    import { createEventDispatcher } from 'svelte'
    //  Methods
    const dispatch = createEventDispatcher()
</script>

<div class="absolute top-0 h-screen w-screen flex justify-center items-center bg-white/50">
    <div class="bg-white py-5 rounded-lg shadow">
        <div class="flex justify-between p-3">
            <slot name="title" />
            <span class="cursor-pointer" on:click={() => dispatch('closeModal')}>
				<i class="bi bi-x-lg"></i>
            </span>
        </div>

		<hr/>

        <slot name="body" />

        <slot name="footer" />
    </div>
</div>
