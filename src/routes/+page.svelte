<script>
	import Header from "./Header.svelte";
	import Nav from "./Nav.svelte";

</script>
<div class="">
    <Nav />
    <Header />
</div>
<style lang="postcss">
    :global(html) {
      background-color: theme(colors.gray.100);
    }
</style>