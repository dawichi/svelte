<script lang="ts">
    import Counter from './components/Counter.svelte'
    import Header from './components/Header.svelte'
    import TailwindCSS from './components/Tailwindcss.svelte'
    import Note from './components/Note.svelte'
</script>

<TailwindCSS />

<header>
	<Header />
</header>

<main>
    <Counter />


	<div class="container mx-auto p-4 rounded grid gap-4 grid-cols-4 bg-zinc-200">
		<Note
			id={1234}
			title={'Some Note'}
			content={'This note is about this and that'}
			tags={['test', 'text']}
			date={'20210806120000'}
			isFavorite={true}
		/>
		<Note
			id={1234}
			title={'Some Note'}
			content={'This note is about this and that'}
			tags={['test', 'text']}
			date={'20210806120000'}
			isFavorite={true}
		/>
	</div>

</main>

<footer>
	footer
</footer>
