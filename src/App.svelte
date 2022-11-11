<script lang="ts">
    import Router from 'svelte-spa-router'
    import Display from './display/Display.svelte'
    import Home from './home/Home.svelte'
</script>

<Router
    routes={{
        '/': Home,
        '/skip': Home,
        '/display/:number': Display,
        '/display/skip/:number': Display
    }}
/>
