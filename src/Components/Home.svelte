<script>
  import firebase from 'firebase/app';
  import { initAuth } from '../auth';

  import Login from './Login.svelte'
  import Dashboard from './Dashboard.svelte'

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

  if (!firebase.apps.length) {
    firebase.initializeApp(firebaseConfig);
  }else {
    firebase.app(); // if already initialized, use that one
  }

  const { loginWithEmailPassword, loginWithGoogle, logout, user } = initAuth();

</script>

<div class="wrapper">
  {#if $user}
    <Dashboard />
  {:else}
    <Login />
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
