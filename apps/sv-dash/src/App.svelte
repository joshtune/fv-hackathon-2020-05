<script lang="ts">
  import { Router, Route, Link } from "svelte-navigator";
  import DocForm from "./doc-form/DocForm.svelte";
</script>

<Router>
  <nav class="navigation">
    <div class="item">
      <Link to="/">Home</Link>
    </div>
    <div class="item">
      <Link to="/doc-form">Doc Form</Link>
    </div>
  </nav>
  <main>
    <Route path="/">
      Home
    </Route>

    <Route path="/doc-form">
      <DocForm />
    </Route>

  </main>
</Router>

<style>
  .navigation {
    padding: 10px;
    margin-bottom: 10px;
    border-bottom: 1px solid #cccccc;
  }

  .item {
    display: inline-block;
    padding-right: 5px;
    color: white;
  }
</style>
