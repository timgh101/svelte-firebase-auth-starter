<script>
	import { getAuth, createUserWithEmailAndPassword } from 'firebase/auth';
	import { onMount } from 'svelte';

	let auth;
	let form;

	onMount(() => {
		auth = getAuth();
		form = document.querySelector('form#signup-form');
		console.log(form);
	});

	function signup(e) {
		e.preventDefault();
		const email = document.querySelector('#signup_email').value;
		const password = document.querySelector('#signup_password').value;

		createUserWithEmailAndPassword(auth, email, password)
			.then((userCredential) => {
				// Signed in
				const user = userCredential.user;
				console.log(user);
				// ...
			})
			.catch((error) => {
				const errorCode = error.code;
				const errorMessage = error.message;
				console.log(error);
				// ..
			});
	}
</script>

<section class="login">
	<form action="" id="signup-form" on:submit={signup}>
		<h1>Signup</h1>
		<label for="email">Email</label>
		<input type="email" name="email" id="signup_email" />
		<label for="password">Password</label>
		<input type="password" name="password" id="signup_password" />
		<button>Submit</button>
	</form>
</section>

<style>
	section.login {
		display: grid;
		place-items: center;
		height: 100vh;
	}
</style>
