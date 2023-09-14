<script>
  import "../app.css";

  const navLinks = [
    { "href": "/", "linkText": "Lotus Planner" },
    { "href": "/about", "linkText": "About" }
  ];
  let drawerOpen = false;

  function onNav() {
    drawerOpen = false;
  }
</script>

<div class="drawer">
  <input id="nav-drawer" type="checkbox" bind:checked={drawerOpen} class="drawer-toggle" />
  <div class="drawer-content">
    <div class="flex-none hamburger-container">
      <label for="nav-drawer" class="btn btn-square btn-ghost drawer-button">
        <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 20 20" class="inline-block w-5 h-5 stroke-current">
          <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16"></path>
        </svg>
      </label>
    </div>
    <slot />
  </div> 
  <div class="drawer-side">
    <label for="nav-drawer" class="drawer-overlay"></label>
    <ul class="menu p-4 w-80 min-h-full bg-base-200 text-base-content">
      {#each navLinks as link}
        <li>
          <a href={link.href} on:click={onNav}>{link.linkText}</a>
        </li>
      {/each}
    </ul>
  </div>
</div>

<style lang="postcss">
  :global(html) {
    /* TODO: This background color definition is broken upon adding DaisyUI to tailwind.config.js. Configure using DaisyUI. */
    background-color: #CCD6EB;
  }

  .hamburger-container {
    /* background-color: #CCD6EB; */
    max-width: 52px;
    height: 52px;
    max-height: 52px;
  }
</style>
