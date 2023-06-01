<script>
	import Navbar from "../../components/navbar.svelte";
	import Productcard from "../../components/productcard.svelte";
	import { browser } from "$app/environment"
	let loggedin
	if(browser)
	 loggedin = localStorage.getItem('login')
</script>

<Navbar/>
<h1 class="ms-5 py-4">All products</h1>
{#if loggedin}
<Productcard/>
{:else}
<h1>Please Login</h1>
{/if}