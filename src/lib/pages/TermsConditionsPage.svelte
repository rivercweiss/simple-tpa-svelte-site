<script>
  import { onMount } from 'svelte';

  let isVisible = $state(false);
  let sectionRef;

  onMount(() => {
    const observer = new IntersectionObserver(
      (entries) => {
        entries.forEach((entry) => {
          if (entry.isIntersecting) {
            isVisible = true;
          }
        });
      },
      { threshold: 0.1 }
    );

    if (sectionRef) {
      observer.observe(sectionRef);
    }

    return () => {
      if (sectionRef) {
        observer.unobserve(sectionRef);
      }
    };
  });
</script>

<section bind:this={sectionRef} class="terms-conditions">
  <div class="hero-section section">
    <div class="container">
      <div class="hero-content" class:animate={isVisible}>
        <h1 class="hero-title">Terms & Conditions</h1>
        <p class="hero-description">
          Last updated: February 2025
        </p>
      </div>
    </div>
  </div>

  <div class="content-section section">
    <div class="container">
      <div class="content">
        <h2>Acceptance of Terms</h2>
        <p>By accessing and using SimpleTPA's services, you accept and agree to be bound by the terms and provision of this agreement.</p>
        
        <h2>Service Description</h2>
        <p>SimpleTPA provides healthcare administration services including benefit management, claims processing, and provider network management.</p>
        
        <h2>User Responsibilities</h2>
        <p>Users are responsible for maintaining the confidentiality of their account information and for all activities that occur under their account.</p>
        
        <h2>Limitation of Liability</h2>
        <p>SimpleTPA shall not be liable for any direct, indirect, incidental, special, or consequential damages arising from the use of our services.</p>
      </div>
    </div>
  </div>
</section>

<style>
  .terms-conditions {
    padding-top: 0;
  }

  .hero-section {
    background: linear-gradient(135deg, var(--color-bg-primary) 0%, var(--color-bg-secondary) 100%);
    padding-top: var(--space-32);
  }

  .hero-content {
    text-align: center;
    max-width: 800px;
    margin: 0 auto;
    opacity: 0;
    transform: translateY(30px);
    transition: all 0.8s ease-out;
  }

  .hero-content.animate {
    opacity: 1;
    transform: translateY(0);
  }

  .hero-title {
    font-size: var(--text-4xl);
    font-weight: var(--font-weight-bold);
    color: var(--color-text-primary);
    margin-bottom: var(--space-6);
  }

  .hero-description {
    font-size: var(--text-lg);
    color: var(--color-text-secondary);
  }

  .content-section {
    background-color: var(--color-bg-primary);
  }

  .content {
    max-width: 800px;
    margin: 0 auto;
  }

  .content h2 {
    color: var(--color-text-primary);
    margin-bottom: var(--space-4);
    margin-top: var(--space-6);
  }

  .content p {
    color: var(--color-text-secondary);
    line-height: var(--leading-relaxed);
    margin-bottom: var(--space-4);
  }
</style>