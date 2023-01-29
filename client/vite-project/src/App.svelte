<script lang="ts">
  import ExerciseDetails from "./pages/ExerciseDetails.svelte";
  import { Router, Route } from "svelte-routing";
  import Home from "./pages/Home.svelte";
  import Navbar from "./components/Navbar.svelte";
  import Footer from "./components/Footer.svelte";
  export let URL: string = "";
</script>

<Router url={URL}>
  <Navbar />
  <main>
    <Route path="" component={Home} />
    <Route path="exercise/:id" let:params>
      <ExerciseDetails id={params.id} />
    </Route>
  </main>
  <Footer/>
</Router>

<main />
