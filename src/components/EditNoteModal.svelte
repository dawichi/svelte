<script lang="ts">
    //  Global Imports
    import moment from 'moment'
    import { createEventDispatcher, onMount } from 'svelte'
    import Modal from './components/Modal.svelte'
    import { formatDate } from '../libs/utils'
    
	//  Props
    export let id: number | undefined = undefined
    export let title: string | undefined = undefined
    export let date: string | undefined = undefined
    export let content: string | undefined = undefined
    export let isFavorite: boolean | undefined = undefined
    export let tags: string[] | undefined = undefined

    //  Varaible Declarations
    let tagString = tags && tags.length ? tags.join(',') : ''
    
	// Simple validation
    $: canSave = Boolean(title && content)

	//  Methods
    const dispatch = createEventDispatcher()

	/**
     * Save the note if allowed by dispatching a save event
     * with the new memo object
     */
    const saveNote = () => {
        if (!canSave) return
        const newMemo = {
            id,
            title,
            content,
            date: moment().format('YYYYMMDDHHmmss'),
            isFavorite,
            tags: tagString
                .replace(/\s/g, '')
                .split(',')
                .filter(item => item),
        }
        if (!newMemo.id) {
            newMemo.id = moment().valueOf()
        }
        dispatch('save', newMemo)
    }

	//  TextArea Resizing
    let textarea: HTMLElement
    const onInput = () => {
        if (textarea) {
            textarea.style.height = 'auto'
            textarea.style.height = `${textarea.scrollHeight}px`
        }
    }

	onMount(() => {
        onInput()
    })
</script>

<Modal on:closeModal={() => dispatch('close')}>
    <div slot="title" class="title">{id ? 'Edit' : 'Create'} Post</div>

    <div slot="body" class="w-96 p-4 grid grid-cols-2">
        <label class="label" for="note-title">Title:</label>
        <input bind:value={title} id="note-title" class="input" type="text" />

        <label class="label" for="note-tags">Tags:</label>
        <input bind:value={tagString} id="note-tags" class="input" type="text" />

        <label class="label" for="note-content">Content:</label>
        <textarea id="note-content" bind:this={textarea} bind:value={content} class="input" type="textarea" on:input={onInput} />

        {#if date}
            <div class="label">Last Updated:</div>
            <div class="text">{formatDate(date)}</div>
        {/if}
    </div>

    <div slot="footer" class="flex justify-between">
        <div class="delete-wrapper">
            {#if id}
                <button class="button delete" on:click|stopPropagation={() => dispatch('delete', id)}> Delete </button>
            {/if}
        </div>
        <div class="buttons-wrapper">
            <button class="button save {!canSave ? 'disabled' : ''}" on:click|stopPropagation={saveNote}> Save </button>
            <button class="button" on:click|stopPropagation={() => dispatch('close')}> Cancel </button>
        </div>
    </div>
</Modal>
