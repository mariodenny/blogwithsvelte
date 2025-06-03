<script>
  import 'bootstrap/dist/css/bootstrap.min.css'
  import { onMount } from 'svelte';

  onMount(async () => {
    await import('bootstrap/dist/js/bootstrap.bundle.min.js')
  })
</script>

<style>
  html, body, #app {
    height: 100%;
  }

  .layout-wrapper {
    display: flex;
    flex-direction: column;
    min-height: 100vh;
  }

  main {
    flex: 1;
  }
</style>

<div class="layout-wrapper">
  <!-- Navbar -->
  <nav class="navbar navbar-expand-lg text-white" style="background-color: #4300FF;" data-bs-theme="dark">
    <div class="container-fluid">
      <a class="navbar-brand" href="/">Navbar</a>
      <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent"
        aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav ms-auto mb-2 mb-lg-0">
          <li class="nav-item">
            <a class="nav-link active" aria-current="page" href="/">Home</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="/admin">Blog</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="/about">About</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="/news">News</a>
          </li>
        </ul>
      </div>
    </div>
  </nav>

  <!-- Main content -->
  <main class="container my-4">
    <slot />
  </main>

  <!-- Footer -->
  <footer class="text-center text-white py-3" style="background-color:#4300FF;">
    <div style="background-color: rgba(0, 0, 0, 0.05);">
      © 2025 Copyright: denny@Kodingnext
      <a class="text-body" href="https://mdbootstrap.com/">MDBootstrap.com</a>
    </div>
  </footer>
</div>
