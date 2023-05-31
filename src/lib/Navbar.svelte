<script lang="ts">
  import { link } from "svelte-routing";
  import MediaQuery from "svelte-media-queries";
  import { slide, fade } from "svelte/transition";

  let navBarOpen = false;
  let showServices = false;

  const close = () => (navBarOpen = false);
  const closeServices = () => (showServices = false);
</script>

<MediaQuery query="(max-width: 800px)" let:matches>
  {#if matches}
    <!-- svelte-ignore a11y-invalid-attribute -->
    <a
      use:link
      class="list-link"
      on:click="{() => (navBarOpen = !navBarOpen)}"
      href="#"
    >
      <svg
        xmlns="http://www.w3.org/2000/svg"
        width="32"
        height="32"
        viewBox="0 0 16 16"
        ><path
          fill="none"
          stroke="#222"
          stroke-linecap="round"
          stroke-linejoin="round"
          stroke-width="1.5"
          d="M2.75 12.25h10.5m-10.5-4h10.5m-10.5-4h10.5"></path></svg
      >
    </a>
    {#if navBarOpen}
      <nav class="nav-mobile" in:slide out:slide>
        <ul>
          <li>
            <a use:link on:click="{close}" class="list-link" href="/">Home</a>
          </li>
          <li>
            <!-- svelte-ignore a11y-invalid-attribute -->
            <a use:link on:click="{close}" class="list-link" href="#"
              >Services</a
            >
            <ul class="inner-nav">
              <li>
                <a
                  use:link
                  on:click="{close}"
                  class="list-link"
                  href="/brush-clearing">Forestry Mulching</a
                >
              </li>
              <li>
                <a use:link on:click="{close}" class="list-link" href="/grading"
                  >Grading and Excavating</a
                >
              </li>
              <li>
                <a
                  use:link
                  on:click="{close}"
                  class="list-link"
                  href="/land-clearing">Land Clearing</a
                >
              </li>
              <li>
                <a
                  use:link
                  on:click="{close}"
                  class="list-link"
                  href="/tree-removal">Tree Service</a
                >
              </li>
            </ul>
          </li>
          <li>
            <a
              use:link
              on:click="{close}"
              class="list-link"
              href="/reviews/"
              aria-current="page">Reviews</a
            >
          </li>
          <li>
            <a use:link on:click="{close}" class="list-link" href="/about-us/"
              >About Us</a
            >
          </li>
          <li>
            <a
              use:link
              on:click="{close}"
              href="/contact-us/"
              class="contact-us">Contact Us</a
            >
          </li>
        </ul>
      </nav>
    {/if}
  {:else}
    <nav class="nav-desktop">
      <a use:link class="desktop-link" href="/">Home</a>
      <div class="dropdown">
        <!-- svelte-ignore a11y-invalid-attribute -->
        <a use:link class="desktop-link dropbtn" href="#">Services</a>
        <ul class="desktop-service-links dropdown-content" in:fade out:fade>
          <li>
            <a
              use:link
              on:click="{closeServices}"
              class="list-link"
              href="/brush-clearing">Forestry Mulching</a
            >
          </li>
          <li>
            <a
              use:link
              on:click="{closeServices}"
              class="list-link"
              href="/grading">Grading and Excavating</a
            >
          </li>
          <li>
            <a
              use:link
              on:click="{closeServices}"
              class="list-link"
              href="/land-clearing">Land Clearing</a
            >
          </li>
          <li>
            <a
              use:link
              on:click="{closeServices}"
              class="list-link"
              href="/tree-removal">Tree Service</a
            >
          </li>
        </ul>
      </div>
      <a use:link class="desktop-link" href="/reviews"> Reviews </a>
      <a use:link class="desktop-link" href="/about-us"> About Us </a>
      <a use:link class="desktop-link contact-us-desktop" href="/contact-us">
        Contact Us
      </a>
    </nav>
  {/if}
</MediaQuery>

<style>
  .contact-us {
    display: block;
    text-decoration: none;
    color: #222222;
    background: #fff;
    padding: 8px 0px 8px 8px;
    font-weight: 600;
    transition: linear 0.25s all;
    width: 99%;
    border: 3px solid #85612a;
  }
  .contact-us:hover {
    background-color: #85612a;
  }
  .nav-mobile {
    position: absolute;
    z-index: 10;
    top: 118px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    border-top: 3px solid #222;
    width: 80%;
    margin: auto;
    background-color: #fff;
    padding: 20px 12px 8px 8px;
  }
  .nav-mobile ul {
    display: flex;
    flex-direction: column;
    list-style: none;
    background-color: #eee;
    width: 95%;
  }
  .nav-mobile ul li {
    text-align: left;
    font-size: 15px;
    width: 100%;
  }
  .nav-mobile ul li .list-link {
    display: block;
    text-decoration: none;
    border-bottom: 1px solid #ddd;
    color: #222222;
    background: #fff;
    padding: 8px 0px 8px 8px;
    font-weight: 600;
    transition: linear 0.25s all;
    width: 100%;
  }
  .nav-mobile ul li .list-link:hover {
    background: #eee;
  }
  .nav-mobile ul li .inner-nav a {
    padding-left: 30px;
  }
  .nav-desktop {
    display: flex;
    align-items: center;
  }
  .desktop-link {
    color: #222;
    margin: 0 10px;
    text-decoration: none;
    font-weight: 600;
    text-transform: uppercase;
    transition: linear 0.25s all;
    width: max-content;
    padding: 30px 0;
  }
  .desktop-link:hover {
    color: #444;
  }
  .contact-us-desktop {
    padding: 8px;
    text-align: center;
    font-weight: 600;
    transition: linear 0.25s all;
    border: 3px solid #85612a;
  }
  .contact-us-desktop:hover {
    background-color: #85612a;
  }
  .desktop-service-links {
    display: flex;
    flex-direction: column;
    align-items: left;
    justify-content: left;
    width: 300px;
    margin: auto;
    padding: 0 16px 0 0;
    background-color: #fff;
    list-style-type: none;
  }

  .desktop-service-links li .list-link {
    display: block;
    text-decoration: none;
    border-bottom: 1px solid #ddd;
    color: #222222;
    background: #fff;
    padding: 16px 0 16px 16px;
    font-weight: 600;
    transition: linear 0.25s all;
    width: 100%;
  }
  .desktop-service-links li .list-link:hover {
    background: #eee;
  }

  .dropdown {
    position: relative;
    display: inline-block;
  }

  .dropdown-content {
    display: none;
    position: absolute;
    top: 50px;
    box-shadow: 0px 8px 16px 0px rgba(0, 0, 0, 0.2);
  }

  .dropdown:hover .dropdown-content {
    display: block;
  }
</style>
