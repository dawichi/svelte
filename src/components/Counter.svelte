<script lang="ts">
    let count: number = 0
    const increment = () => {
        count += 1
    }
</script>

<button class="bg-red-400 py-1 px-2 rounded-lg" on:click={increment}>
    Clicks: {count}
</button>
