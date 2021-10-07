<script>
	import { onMount } from 'svelte';
	import { getAuth, signInWithEmailAndPassword } from 'firebase/auth';

	let auth;

	onMount(() => {
		const auth = getAuth();
	});

	function signin() {
		const email = document.querySelector('#login-email-input').value;
		const password = document.querySelector('#login-password-input').value;
		signInWithEmailAndPassword(auth, email, password)
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
			});
	}
</script>

<section class="login">
	<form action="" id="login-form" on:submit={signin}>
		<h1>login</h1>
		<label for="email">email</label>
		<input type="email" name="email" id="login-email-input" />
		<label for="password">password</label>
		<input type="password" name="password" id="login-password-input" />
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
