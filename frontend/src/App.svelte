<script lang="ts">
  import { Router, Route, link } from "svelte-routing";
  import Menu from "./routes/Menu.svelte";
</script>

<nav>
  <a href="/" use:link><h1>boring</h1></a>
  <div>
    <a class="button button-alt" href="/about">About us</a>
    <a
      class="button"
      target="_blank"
      href="https://github.com/WardPearce/boring">Github</a
    >
  </div>
</nav>

<Router>
  <Route path="/" component={Menu} />
</Router>
