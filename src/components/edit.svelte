<script>
    let editId = ``
    let productDetails = {
        name:'',
        price: ``,
        id:``
    }
     async function store(){
		await fetch(`http://localhost:3000/products/${editId}`, {
			method: 'PUT',
			headers: { 'Content-Type': 'application/json' },
			body: JSON.stringify(productDetails)
		})
		.then((res) => res.json())
		.then(console.log)
        alert('Product Edited Succesfully')
    }
</script>

<form class="w-50 mx-auto">
	<h3 class="text-center py-5">Edit a Product</h3>
	<div class="mb-3">
		<label for="exampleInputEmail1" class="form-label">Product Name</label>
		<input type="text" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp" bind:value={productDetails.name} />
	</div>
	<div class="mb-3">
		<label for="exampleInputPassword1" class="form-label">Price</label>
		<input type="number" class="form-control" id="exampleInputPassword1" bind:value={productDetails.price}/>
	</div>
	<div class="mb-3">
		<label for="exampleInputPassword1" class="form-label">Id</label>
		<input type="number" class="form-control" id="exampleInputPassword1" bind:value={editId}/>
	</div>
	<button type="submit" class="btn btn-primary" on:click={store}>Save</button>
</form>
