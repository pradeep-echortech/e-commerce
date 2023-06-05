<script>
	import Navbar from "../../components/navbar.svelte";
	import Productcard from "../../components/productcard.svelte";
	let loggedinuser;
	(() => {
		if (typeof window == 'undefined') return;
		loggedinuser = localStorage.getItem('loginuser');
	})();
</script>

{#if loggedinuser}
<Navbar/>
<h1 class="ms-5 py-4">All products</h1>
<Productcard/>
{/if}
{#if !loggedinuser}
<h1 class="m-5">Please Login to get access</h1>
<a class="btn btn-primary text-center mx-5 " href="/login">Login</a>
{/if}