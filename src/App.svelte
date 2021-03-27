<script>
	import firebase from 'firebase/app';
	import { initAuth } from './auth';
	import { fade } from 'svelte/transition';

	const firebaseConfig = {
		apiKey: "AIzaSyCyNa9YxHq3n1Fw0r09H2bZMtzVJ95eZAk",
		authDomain: "dg-invoices.firebaseapp.com",
		databaseURL: "https://dg-invoices-default-rtdb.firebaseio.com",
		projectId: "dg-invoices",
		storageBucket: "dg-invoices.appspot.com",
		messagingSenderId: "439675326689",
		appId: "1:439675326689:web:24bf8e1c9535f78faee7a0",
		measurementId: "G-73VWEZ5VCM"
	};

	firebase.initializeApp(firebaseConfig);

	const { loginWithEmailPassword, loginWithGoogle, logout, user } = initAuth();

	let error = null;

	const loginHandler = async event => {
		const { email, password } = event.target.elements;
		try {
			error = null;
			await loginWithEmailPassword(email.value, password.value);
		} catch (err) {
			error = err;
		}
	};
</script>

<div class="wrapper">
	{#if $user}
		<div class="w-full max-w-xs">
			<div class="text-center">
				<h2>{$user.email}</h2>
				<button type="button" class="mt-3" on:click={logout}>Logout</button>
			</div>
		</div>
	{:else}
		<div class="w-full max-w-xs">
			<form
					on:submit|preventDefault={loginHandler}
					class="px-8 pt-6 pb-8 bg-white shadow-md"
			>
				<div class="mb-4">
					<label for="email">Email</label>
					<input
							class="input-field"
							id="email"
							type="email"
							placeholder="name@acme.com"
					/>
				</div>
				<div class="mb-6">
					<label for="password">Password</label>
					<input
							class="input-field"
							id="password"
							type="password"
							placeholder="******************"
					/>
				</div>
				{#if error}
					<div transition:fade class="p-2 mb-6 bg-red-300">{error.message}</div>
				{/if}
				<div>
					<button type="submit">Sign In</button>
				</div>
				<div class="mt-3">
					<button type="button" on:click|preventDefault={loginWithGoogle}>
						Sign In with Google
					</button>
				</div>
			</form>
		</div>
	{/if}
</div>

<style lang="scss">
	.wrapper {
		background-color: pink;
		padding: 15px;

		button {
			background-color: lightcoral;
			color: white;
		}
	}
</style>
