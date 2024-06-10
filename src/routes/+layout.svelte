<script lang="ts">
  import NavBar from "$lib/components/NavBar.svelte";
  import { user, userData } from "$lib/firebase";
  import "../app.css";

  $user;
  $userData;
</script>

<div class="min-h-screen flex flex-col">
  <NavBar />
  <div class="mb-12 pb-12">
    <slot />
  </div>
</div>
