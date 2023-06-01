<script>
    let deleteId 
    async function store(){
		await fetch(`http://localhost:3000/products/${deleteId}`, {
			method: 'Delete',
		})
		.then((res) => res.json())
		.then(console.log)
        alert('Product Deleted Succesfully')
    }
</script>

<form class="w-50 mx-auto">
    <h3 class="text-center py-5">Delete a Product</h3>
    <div class="mb-3">
      <label for="exampleInputPassword1" class="form-label">Enter the Id</label>
      <input type="number" class="form-control" id="exampleInputPassword1" bind:value={deleteId}>
    </div>
    <button type="submit" class="btn btn-primary" on:click={store}>Delete</button>
  </form>