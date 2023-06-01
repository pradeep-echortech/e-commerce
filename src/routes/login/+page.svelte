<script>
    import Defaultnav from "../../components/defaultnav.svelte";
	import {goto} from  '$app/navigation'
	let userLoggedin= false;
	let login = {
		username:'',
		password:'',
	}
    export async function check() {
        fetch('http://localhost:3000/users')
        .then(res=>res.json())
        .then(value => {
			value.forEach(element => {
				if(element.username == login.username && element.password == login.password)
				{
					let details = [element.id,element.username]
					console.log('Welcome !');
					 goto('/products')
					 userLoggedin = true
					 localStorage.setItem('login',userLoggedin)
					 localStorage.setItem('loginuser',details)
				}
				else{
					console.log('Invalid Login Details');
					// userLoggedin = false
				}
			});
		})
    }

	
</script>

<Defaultnav/>
<div class="container">
	<div class="row d-flex justify-content-center">
		<div class=" py-5 text-center">
			<h2>Login Page</h2>
		</div>
		<form class="col-5 " id="myform">
			<div class="mb-3 ">
				<label for="exampleInputEmail1" class="form-label">User Name</label>
				<input
					type="text"
					class="form-control"
					id="exampleInputEmail1"
					aria-describedby="emailHelp"
					bind:value={login.username}
				/>
			</div>
			<div class="mb-3 ">
				<label for="exampleInputPassword1" class="form-label">Password</label>
				<input type="password" class="form-control" id="exampleInputPassword1" bind:value={login.password} />
			</div>
			<button type="submit" class="btn btn-primary" on:click={check}>Login</button>
		</form>
		<div class="py-4 text-center">
			<h6>New User? <a href="/register">Register</a></h6>
		</div>
	</div>
</div>
