<script>
	import { browser } from "$app/environment"
	(async () => {
		let res = await fetch('http://localhost:3000/userproducts')
			.then((res) => res.json())
			.then((res) => res);
		crdbody = [...res];
		// console.log(crdbody[0].userid);
	})();
	let crdbody = [];

	function remove(id) {
		fetch(`http://localhost:3000/userproducts/${id}`, {
			method: 'DELETE'
		})
			.then((res) => res.json())
			.then(console.log);
		location.reload();
	}

	let loggedinUser
	if(browser){
		 loggedinUser = localStorage.getItem('loginuser');
	}

	// let loggedinUser;
	// (() => {
	// 	if (typeof window == 'undefined') return;
	// 	loggedinUser = localStorage.getItem('loginuser');
	// })();
</script>

<div class="d-flex justify-content-end">
	<a class="btn btn-success mx-3 mt-3" href="/">Home</a>
	<a class="btn btn-success mx-3 mt-3" target="_blank" href="/checkout">Checkout</a>
</div>
<h1 class="ms-4">Your cart<i class="fa-solid fa-cart-shopping mx-1" /></h1>

<div class="container justify-content-center">
	<div class="container d-flex flex-wrap justify-content-center">
		{#each crdbody as bdy}
			{#if loggedinUser?.[0] == bdy.userid}
				<div class="card" style="width: 14rem;padding: 5px;margin: 5px;height: 290px;">
					<!-- <a href='/products/{bdy.id}' class="ms-auto me-3"><i class="fa-solid fa-arrow-right"></i></a> -->
					<div class="card-body" style="line-height:13px ">
						<h1 class="card-title">{bdy.name}</h1>
						<p class="card-text">Price :${bdy.price}</p>
						<p class="card-text">User Id:{bdy.userid}</p>
						<button class="btn btn-danger" id={bdy.id} on:click={remove(bdy.id)}>Remove</button>
					</div>
				</div>
			{/if}
		{/each}
	</div>
</div>
