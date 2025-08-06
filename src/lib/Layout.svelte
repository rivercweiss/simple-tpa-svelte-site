<script>
  import Header from './Header.svelte';
  import Footer from './Footer.svelte';

  let { children } = $props();
</script>

<div class="layout">
  <Header />
  <main class="main">
    {@render children()}
  </main>
  <Footer />
</div>

<style>
  .layout {
    min-height: 100vh;
    display: flex;
    flex-direction: column;
  }

  .main {
    flex: 1;
    padding-top: var(--total-header-height);
  }
</style>