<script>
  import { auth, userData } from "$lib/firebase";
  import { signOut } from "firebase/auth";

  async function signOutSSR() {
    const res = await fetch("/api/signin", { method: "DELETE" });
    await signOut(auth);
  }
</script>

<div class="navbar bg-base-100">
  <div class="navbar-start">
    <div class="dropdown">
      <div tabindex="0" role="button" class="btn btn-ghost lg:hidden">
        <svg
          xmlns="http://www.w3.org/2000/svg"
          class="h-5 w-5"
          fill="none"
          viewBox="0 0 24 24"
          stroke="currentColor"
          ><path
            stroke-linecap="round"
            stroke-linejoin="round"
            stroke-width="2"
            d="M4 6h16M4 12h8m-8 6h16"
          /></svg
        >
      </div>
      {#if $userData?.username}
        <!-- svelte-ignore a11y-no-noninteractive-tabindex -->
        <ul
          tabindex="0"
          class="menu menu-sm dropdown-content mt-3 z-[1] p-2 shadow bg-base-100 rounded-box w-52"
        >
          <li><a href="/{$userData.username}">Profile</a></li>
          <li><a href="/{$userData.username}/edit">Edit</a></li>
        </ul>
      {/if}
    </div>
    <a class="btn btn-ghost text-xl" href="/">Link Page</a>
  </div>
  {#if $userData?.username}
    <div class="navbar-center hidden lg:flex">
      <ul class="menu menu-horizontal px-1">
        <li>
          <a href="/{$userData.username}">
            <img
              src={`/profile.png`}
              alt="profile icon"
              width="24"
              height="24"
            />
            Profile</a
          >
        </li>
        <li>
          <a href="/{$userData.username}/edit">
            <img src={`/edit.png`} alt="edit icon" width="24" height="24" />
            Edit</a
          >
        </li>
      </ul>
    </div>
    <div class="navbar-end">
      <a class="btn btn-outline btn-xs" href="/" on:click={signOutSSR}
        >Sign Out</a
      >
    </div>
  {/if}
</div>
