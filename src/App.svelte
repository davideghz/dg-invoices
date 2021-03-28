<script>
	import { Router, Link, Route } from "svelte-routing";
	import Home from "./Components/Home.svelte";
	import About from "./Components/About.svelte";

	export let url = "/";
</script>

<Router url="{url}">
	<nav>
		<Link to="">Home</Link>
		<Link to="about">About</Link>
		<Link to="blog">Blog</Link>
	</nav>
	<div>
		<Route path="/"><Home /></Route>
		<Route path="about"><About /></Route>
	</div>
</Router>
