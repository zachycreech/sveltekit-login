<script lang="ts">
	import { authHandlers } from '$store/store';

	authHandlers;
	let email = '';
	let password = '';
	let confirmPassword = '';
	let error = false;
	let register = false;
	let authenticating = false;

	async function handleAuthenticate() {
		if (authenticating) return;

		if (!email || !password || (register && !confirmPassword)) return (error = true);

		authenticating = true;

		try {
			if (register) {
				if (password !== confirmPassword) return (error = true);
				await authHandlers.signup({ email, password });
			} else {
				await authHandlers.login({ email, password });
			}
		} catch (e) {
			console.error(e);
			error = true;
			authenticating = false;
		}

		authenticating = true;
	}
	function handleRegister() {
		register = !register;
	}
</script>

<div class="authContaner">
	<form>
		<h1>{register ? 'Register' : 'Login'}</h1>
		{#if error}
			<p style="color: red;">The information you have provided is not correct.</p>
		{/if}
		<label>
			<p class={email ? 'above' : 'center'}>Email</p>
			<input autocomplete="off" bind:value={email} type="email" placeholder="Email" />
		</label>
		<label>
			<p class={password ? 'above' : 'center'}>Password</p>
			<input autocomplete="off" bind:value={password} type="password" placeholder="Password" />
		</label>
		{#if register}
			<label>
				<p class={confirmPassword ? 'above' : 'center'}>Confirm Password</p>
				<input bind:value={confirmPassword} type="password" placeholder="Confirm Password" />
			</label>
		{/if}
		<button on:click={handleAuthenticate} type="button">Submit</button>
	</form>
	<div class="options">
		{#if register}
			<div>
				<p>Already have an account?</p>
				<button class="link" on:click={handleRegister}>Login</button>
			</div>
		{:else}
			<div>
				<p>Don't have an account?</p>
				<button class="link" on:click={handleRegister}>Register</button>
			</div>
		{/if}
	</div>
</div>

<style>
	.authContaner {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		flex: 1;
	}

	form {
		--size: 400px;
		display: flex;
		flex-direction: column;
		gap: 0.7rem;
		width: var(--size);
		margin: 0 auto;
		max-width: 100%;
		inset: calc(50% - calc(var(--size) / 2));
	}

	form input {
		width: 100%;
		border: none;
		color: white;
		background: transparent;
		padding: 0.7rem;
	}

	form input:focus {
		outline: none;
	}

	form label {
		position: relative;
		border: 1px solid purple;
		border-radius: 0.1rem;
	}

	form button {
		background: indigo;
		color: white;
		border: none;
		padding: 0.7rem;
		font-size: 1.2rem;
		margin-bottom: 1rem;
	}

	form button:hover {
		background: rebeccapurple;
		border-radius: 0.1rem;
		cursor: pointer;
	}

	h1 {
		text-align: center;
		font-size: 3rem;
	}
	.above,
	.center {
		position: absolute;
		transform: translateY(-50%);
		pointer-events: none;
		color: white;
		padding: 0 0.4rem;
		border-radius: 0.1rem;
		font-size: 0.8rem;
	}
	.above {
		top: 0;
		left: 24px;
		background: indigo;
		border: 1px solid indigo;
		font-size: 0.8rem;
	}
	.center {
		top: 50%;
		left: 0;
		border: 1px solid transparent;
		opacity: 0;
	}
	.options {
		--size: 396px;
		padding: 1rem;
		width: var(--size);
		gap: 0.7rem;
		position: relative;
		border-top: 1px solid white;
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}
	.link {
		font-size: 1rem;
		background: transparent;
		border: none;
		color: rebeccapurple;
		cursor: pointer;
	}
</style>
