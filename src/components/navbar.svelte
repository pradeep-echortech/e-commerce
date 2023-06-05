<script>
	import { browser } from '$app/environment';
  import {goto} from  '$app/navigation'

  function logout(){
    let loggedinUser;
    if (browser) {
      loggedinUser = localStorage.removeItem('loginuser');
      alert('Successfully Logged out')
      goto('/')
    }
  }
</script>

<nav class="navbar navbar-expand-lg navbar-light bg-warning">
	<div class="container-fluid">
		<a class="navbar-brand" href="/">E-commerce</a>
		<button
			class="navbar-toggler"
			type="button"
			data-bs-toggle="collapse"
			data-bs-target="#navbarSupportedContent"
			aria-controls="navbarSupportedContent"
			aria-expanded="false"
			aria-label="Toggle navigation"
		>
			<span class="navbar-toggler-icon" />
		</button>
		<div class="collapse navbar-collapse" id="navbarSupportedContent">
			<ul class="navbar-nav me-auto mb-2 mb-lg-0">
				<li class="nav-item">
					<a class="nav-link" href="/products">Products</a>
				</li>
				<li class="nav-item">
					<a class="nav-link" href="/about">About us</a>
				</li>
			</ul>

			<a href="/create" target="_blank" class="btn btn-primary mx-3">Create Product</a>
			<a href="/cart" target="_blank" class="btn btn-primary mx-3"
				>My Cart<i class="fa-solid fa-cart-shopping mx-1 fa-beat" /></a
			>
			<button class="btn btn-primary mx-3" on:click={logout}><i class="fa-solid fa-right-from-bracket fa-beat"></i> Logout</button>
		</div>
	</div>
</nav>
