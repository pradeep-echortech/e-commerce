<script>
	import Defaultnav from '../../components/defaultnav.svelte';
	import {goto} from  '$app/navigation'


	let userDetails = {
        id: (i)=>{
            if(i){i+=1}
        },
		username: '',
		password: ''
	};

	function store() {
		fetch('http://localhost:3000/users', {
			method: 'POST',
			headers: { 'Content-Type': 'application/json' },
			body: JSON.stringify(userDetails)
		})
		.then((res) => res.json())
		.then(console.log)
		.then(()=>goto('/login'))
	}
</script>

<Defaultnav />

<div class="container">
	<div class="row d-flex justify-content-center">
		<div class=" py-5 text-center">
			<h2>Register Page</h2>
		</div>
		<form class="col-5">
			<div class="mb-3">
				<label for="exampleInputEmail1" class="form-label">User Name</label>
				<input
					type="text"
					class="form-control"
					id="exampleInputEmail1"
					aria-describedby="emailHelp"
					bind:value={userDetails.username}
				/>
			</div>
			<div class="mb-3">
				<label for="exampleInputPassword1" class="form-label">Password</label>
				<input
					type="password"
					class="form-control"
					id="exampleInputPassword1"
					bind:value={userDetails.password}
				/>
			</div>
			<button type="submit" class="btn btn-primary" on:click={store}>Submit</button>
		</form>
	</div>
</div>
