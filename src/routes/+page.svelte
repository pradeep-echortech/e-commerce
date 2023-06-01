<script>
	import Defaultnav from '../components/defaultnav.svelte';
	let pageno = 1;
	async function Getdatafromjson(page) {
		if(page <= 5){
			let res = await fetch(`http://localhost:3000/products?_page=${page}&_limit=10`)
			.then((res) => res.json())
			.then((res) => res);
			crdbody = [...res];
			pageno += 1;
		}else{
			let res = await fetch(`http://localhost:3000/products?_page=1&_limit=10`)
			.then((res) => res.json())
			.then((res) => res);
			crdbody = [...res];
		}
	}
	async function PreviousPage(page) {
		let res = await fetch(`http://localhost:3000/products?_page=${page-2}&_limit=10`)
		.then((res) => res.json())
		.then((res) => res);
		crdbody = [...res];
		pageno += -1;
	}
	(async () => {
		Getdatafromjson();
	})();
	let crdbody = [];
</script>

<Defaultnav />
<div class="container text-center p-5">
	<h1>Login with your credentials</h1>
</div>

<div class="container justify-content-center">
	<div class="container d-flex flex-wrap justify-content-center">
		{#each crdbody as bdy}
			<div class="card" style="width: 14rem;padding: 5px;margin: 5px;height: 300px;">
				<a href="/products/{bdy.id}" class="ms-auto me-3"><i class="fa-solid fa-arrow-right" /></a>
				<div class="card-body"style="line-height:10px;">
					<h1 class="card-title"> {bdy.name}</h1>
					<p class="card-text">Price : ${bdy.price}</p>
					<p class="card-text">Product id : {bdy.id}</p>
					<a class="btn btn-primary" href="/login">Buy Now</a>
				</div>
			</div>
		{/each}
	</div>
</div>
<div class="d-flex justify-content-center">
	<button class="btn btn-warning mx-3 my-5" on:click={() => PreviousPage(pageno)}><i class="fa-solid fa-arrow-left fa-beat-fade"></i> Previous Page</button>
	<button class="btn btn-warning mx-3 my-5" on:click={() => Getdatafromjson(pageno=1)}><i class="fa-solid fa-house fa-beat-fade"></i> Home Page</button>
	<button class="btn btn-warning mx-3 my-5" on:click={() => Getdatafromjson(pageno)}>Next Page  <i class="fa-solid fa-arrow-right fa-beat-fade"></i></button>
</div>
