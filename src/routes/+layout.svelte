<script>
  import "../app.css";

  // TODO: Fix bug where active link can become out of sync on UI after hard refresh
  let navLinks = [
    { href: "/", linkText: "Lotus Planner", active: true },
    { href: "/about", linkText: "About", active: false }
  ];
  let drawerOpen = false;

  /**
   * @param {{ href: string; linkText: string; active: boolean; }} clickedLink
   */
  function onNav(clickedLink) {
    let activeLink = getActiveLink();

    if (clickedLink.href !== activeLink.href) {
      activeLink.active = false;
      clickedLink.active = true;
      // https://learn.svelte.dev/tutorial/updating-arrays-and-objects
      navLinks = navLinks;
      
      drawerOpen = false;
    }
  }

  function getActiveLink() {
    let activeLink = navLinks.find(link => { return link.active });
    if (!activeLink) throw new Error('Could not find active drawer link');
    return activeLink;
  }
</script>

<div class="drawer h-full">
  <input id="nav-drawer" type="checkbox" bind:checked={drawerOpen} class="drawer-toggle" />
  <div class="drawer-content h-full">
    <div class="flex-none hamburger-container absolute">
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
    <ul class="menu pt-4 pl-0 pr-0 w-80 min-h-full bg-base-200 text-base-content">
      {#each navLinks as link}
        <li>
          <a href={link.href}
            class="{"active"} rounded-none pt-3.5 pl-6 h-12"
            class:active={link.active}
            on:click={() => onNav(link)}>
              {link.linkText}
          </a>
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
