<script>
  import { applyAction, enhance } from "$app/forms";
  import { pb } from "$lib/pocketbase";
</script>

<form
  method="post"
  class="card"
  use:enhance={() => {
    return async ({ result }) => {
      pb.authStore.loadFromCookie(document.cookie);
      await applyAction(result);
    };
  }}
>
  <h1 class="text-2xl mb-8">Form masuk Sederhana</h1>
  <div class="form-control gap-2 mb-4">
    <input
      type="email"
      placeholder="Email"
      name="email"
      class="input input-bordered"
    />
    <input
      type="password"
      placeholder="Password"
      name="password"
      class="input input-bordered"
    />
  </div>
  <button class="btn btn-primary">Login</button>
</form>
