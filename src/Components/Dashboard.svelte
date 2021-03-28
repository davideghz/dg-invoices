<script>
  import { initAuth } from '../auth';
  const { loginWithEmailPassword, loginWithGoogle, logout, user } = initAuth();
</script>

<div>
  <div>
    <h2>{$user && $user.email}</h2>
    <h2>{$user && $user.name}</h2>
    <img src="{$user && $user.picture}" alt="">
    <p>
      <button type="button" class="mt-3" on:click={logout}>Logout</button>
    </p>
  </div>
</div>
