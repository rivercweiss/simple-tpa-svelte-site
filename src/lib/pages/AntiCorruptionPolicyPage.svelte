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

<section bind:this={sectionRef} class="anti-corruption">
  <div class="hero-section section">
    <div class="container">
      <div class="hero-content" class:animate={isVisible}>
        <h1 class="hero-title">Anti-Corruption Policy</h1>
        <p class="hero-description">
          SimpleTPA is committed to conducting business with integrity and in compliance with all applicable laws.
        </p>
      </div>
    </div>
  </div>

  <div class="content-section section">
    <div class="container">
      <div class="content">
        <h2>Our Commitment</h2>
        <p>SimpleTPA has zero tolerance for corruption, bribery, and any form of unethical business practices.</p>
        
        <h2>Prohibited Activities</h2>
        <p>We prohibit all forms of corruption, including but not limited to bribery, kickbacks, and facilitation payments.</p>
        
        <h2>Reporting Violations</h2>
        <p>If you become aware of any violation of this policy, please report it immediately to our compliance team.</p>
        
        <h2>Training and Awareness</h2>
        <p>All employees receive regular training on anti-corruption policies and ethical business practices.</p>
      </div>
    </div>
  </div>
</section>

<style>
  .anti-corruption {
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
    line-height: var(--leading-relaxed);
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