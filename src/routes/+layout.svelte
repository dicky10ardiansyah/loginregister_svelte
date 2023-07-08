<script>
  import "../app.css";
  import { applyAction, enhance } from "$app/forms";
  import { currentUser, pb } from "$lib/pocketbase";
</script>

<div class="bg-neutral text-neutral-content">
  <div class="max-w-4xl mx-auto navbar">
    <div class="navbar-start">
      <a href="/" class="btn btn-ghost normal-case text-xl">CRUD Sederhana</a>
    </div>
    <div class="navbar-end">
      <ul class="menu menu-horizontal">
        <li><a href="/">Home</a></li>
        {#if $currentUser}
          <li><a href="/">{$currentUser.email}</a></li>
          <li>
            <form
              action="/logout"
              method="post"
              use:enhance={() => {
                return async ({ result }) => {
                  pb.authStore.clear();
                  await applyAction(result);
                };
              }}
            >
              <button type="submit">Logout</button>
            </form>
          </li>
        {:else}
          <li><a href="/login">Login</a></li>
          <li><a href="/register">Register</a></li>
        {/if}
      </ul>
    </div>
  </div>
</div>

<div class="max-w-xl mx-auto py-8 px-4">
  <slot />
</div>
