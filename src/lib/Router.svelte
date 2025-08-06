<script>
  import { onMount } from 'svelte';
  
  // Import page components
  import HomePage from './pages/HomePage.svelte';
  import AboutPage from './AboutPage.svelte';
  import HowTPAWorks from './HowTPAWorks.svelte';
  import ContactPage from './pages/ContactPage.svelte';
  import HealthcareProvidersPage from './pages/HealthcareProvidersPage.svelte';
  import SMECorporationsPage from './pages/SMECorporationsPage.svelte';
  import ProviderNetworkPage from './pages/ProviderNetworkPage.svelte';
  import CareersPage from './pages/CareersPage.svelte';
  import PrivacyPolicyPage from './pages/PrivacyPolicyPage.svelte';
  import TermsConditionsPage from './pages/TermsConditionsPage.svelte';
  import AntiCorruptionPolicyPage from './pages/AntiCorruptionPolicyPage.svelte';
  
  let currentPath = $state('');
  
  const routes = {
    '/': HomePage,
    '/about': AboutPage,
    '/how-tpa-works': HowTPAWorks,
    '/contact': ContactPage,
    '/healthcare-providers': HealthcareProvidersPage,
    '/sme-corporations': SMECorporationsPage,
    '/provider-network': ProviderNetworkPage,
    '/careers': CareersPage,
    '/privacy-policy': PrivacyPolicyPage,
    '/terms-conditions': TermsConditionsPage,
    '/anti-corruption-policy': AntiCorruptionPolicyPage
  };
  
  function updatePath() {
    currentPath = window.location.pathname;
    // Scroll to top when path changes
    window.scrollTo({ top: 0, behavior: 'smooth' });
  }
  
  function navigate(path) {
    window.history.pushState({}, '', path);
    updatePath();
  }
  
  // Make navigate function available globally
  if (typeof window !== 'undefined') {
    window.navigate = navigate;
  }
  
  onMount(() => {
    updatePath();
    
    // Handle browser back/forward buttons
    window.addEventListener('popstate', updatePath);
    
    // Handle link clicks
    document.addEventListener('click', (e) => {
      const target = e.target;
      if (target && target.tagName === 'A') {
        if (target.href && target.href.startsWith(window.location.origin)) {
          e.preventDefault();
          const path = new URL(target.href).pathname;
          navigate(path);
        }
      }
    });
    
    return () => {
      window.removeEventListener('popstate', updatePath);
    };
  });
  
  // Use $derived instead of $: for Svelte 5
  const CurrentComponent = $derived(routes[currentPath] || routes['/']);
</script>

{#if CurrentComponent}
  <CurrentComponent />
{/if}