<script>
    import {page} from '$app/stores';
    const productId = $page.params.productId;
    (async () => {
		let res = await fetch('http://localhost:3000/products')
			.then((res) => res.json())
			.then((res) => res);
		crdbody = [...res];
		
	})();
	let crdbody = [];
</script>
<h2 class="mt-2 pb-5">Details about the product {productId}:</h2>
<div class="container d-flex justify-content-center flex-column">
	<div class="d-flex flex-wrap container-fluid justify-content-center" id="cartdisplay">
		{#if crdbody[productId-1]}
			<div class="card" style="width: 14rem;padding: 5px;margin: 5px;">
				<div class="card-body" style="height: fit-content;">
					<h1 class="card-title">Product : {crdbody[productId-1].name}</h1>
					<p class="card-text">Price.{crdbody[productId-1].price}</p>
					<p class="card-text">Description : Lorem ipsum dolor sit amet consectetur, adipisicing elit. Minus tempore nostrum quasi sequi!</p>
					<a class="btn btn-primary" id="product{crdbody[productId-1].id}">Add To Cart</a>
				</div>
			</div>
		{/if}
	</div>
</div>


