<script lang="ts">
    import Counter from './components/Counter.svelte'
    import Header from './components/Header.svelte'
    import Feed from './components/Feed.svelte'

    import './styles/main.css'
</script>

<header>
    <Header />
</header>

<main>
    <Counter />

    <Feed />
</main>

<footer class="bg-zinc-900 text-white p-4 mt-20">
    footer
</footer>
