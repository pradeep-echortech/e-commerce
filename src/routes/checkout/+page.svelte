<script>
	let loggedinUser;
	(() => {
		if (typeof window == 'undefined') return;
		loggedinUser = localStorage.getItem('loginuser');
		console.log(loggedinUser?.[0], 'local storage');
	})();
	(async () => {
		let res = await fetch(`http://localhost:3000/userproducts?userid=${loggedinUser?.[0]}`)
			.then((res) => res.json())
			.then((res) => res);
		crdbody = [...res];
		res.map((val) => (totalCount += val?.price));
	})();
	let crdbody = [];
	let totalCount = 0;
	function remove(id) {
		fetch(`http://localhost:3000/userproducts/${id}`, {
			method: 'DELETE'
		})
			.then((res) => res.json())
			.then(console.log);
		location.reload();
	}
</script>

{#if loggedinUser}
<h1 class="py-3">checkout</h1>

<table class="table" id="check">
	<thead>
		<tr>
			<th scope="col" class="ms-2">Product Id</th>
			<th scope="col">Product Name</th>
			<th scope="col">Price</th>
			<th></th>
		</tr>
	</thead>
	<tbody>
		{#each crdbody as bdy}
			<tr>
				<td>{bdy.productid}</td>
				<td>{bdy.name}</td>
				<td>$ {bdy.price}</td>
				<td><button class="btn btn-danger" on:click={remove(bdy.id)}>Remove</button></td>
			</tr>
		{/each}
	</tbody>
</table>
<div class="d-flex justify-content-end w-100"><h1 class="me-5">Total= $ {totalCount}</h1></div>
{/if}
{#if !loggedinUser}
<h1 class="m-5">Please Login to get access</h1>
<a class="btn btn-primary text-center mx-5" href="/login">Login</a>
{/if}