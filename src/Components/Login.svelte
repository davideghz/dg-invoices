<script>
  import { initAuth } from '../auth';
  import { fade } from 'svelte/transition';

  const { loginWithEmailPassword, loginWithGoogle, logout, user } = initAuth();

  const loginHandler = async event => {
    const { email, password } = event.target.elements;
    try {
      error = null;
      await loginWithEmailPassword(email.value, password.value);
    } catch (err) {
      error = err;
    }
  };

  let error = null;
</script>

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
