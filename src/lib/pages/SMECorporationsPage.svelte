<script>
  import { onMount } from 'svelte';

  let isVisible = $state(false);
  let sectionRef;

  const benefits = [
    {
      icon: '💰',
      title: 'Up to 30% Cost Savings',
      description: 'Reduce healthcare administration costs through our automated platform and efficient processes.'
    },
    {
      icon: '📊',
      title: 'Real-time Analytics',
      description: 'Track healthcare spending, employee utilization, and cost trends with comprehensive dashboards.'
    },
    {
      icon: '⚡',
      title: 'Reduced HR Workload',
      description: 'Automate benefit management, claims processing, and employee enrollment tasks.'
    },
    {
      icon: '🛡️',
      title: 'Compliance Management',
      description: 'Stay compliant with healthcare regulations and government requirements automatically.'
    }
  ];

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

<section bind:this={sectionRef} class="sme-corporations">
  <!-- Hero Section -->
  <div class="hero-section section">
    <div class="container">
      <div class="hero-content" class:animate={isVisible}>
        <h1 class="hero-title">Healthcare Benefits for SMEs & Corporations</h1>
        <p class="hero-description">
          Streamline your healthcare benefits administration while saving up to 30% on costs. 
          Our platform is designed specifically for small to medium enterprises and large corporations.
        </p>
        <div class="hero-cta">
          <a href="/contact" class="btn-primary">Get Started</a>
          <a href="/how-tpa-works" class="btn-secondary">Learn More</a>
        </div>
      </div>
    </div>
  </div>

  <!-- Benefits Grid -->
  <div class="benefits-section section">
    <div class="container">
      <h2 class="section-title text-center">Why Companies Choose SimpleTPA</h2>
      
      <div class="benefits-grid">
        {#each benefits as benefit, index}
          <div class="benefit-card" style="--delay: {index * 0.1}s">
            <div class="benefit-icon">{benefit.icon}</div>
            <h3 class="benefit-title">{benefit.title}</h3>
            <p class="benefit-description">{benefit.description}</p>
          </div>
        {/each}
      </div>
    </div>
  </div>
</section>

<style>
  .sme-corporations {
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

  @media (min-width: 768px) {
    .hero-title {
      font-size: var(--text-5xl);
    }
  }

  .hero-description {
    font-size: var(--text-lg);
    color: var(--color-text-secondary);
    line-height: var(--leading-relaxed);
    margin-bottom: var(--space-8);
  }

  .hero-cta {
    display: flex;
    flex-direction: column;
    gap: var(--space-4);
    align-items: center;
  }

  @media (min-width: 640px) {
    .hero-cta {
      flex-direction: row;
      justify-content: center;
    }
  }

  .benefits-section {
    background-color: var(--color-bg-primary);
  }

  .section-title {
    font-size: var(--text-3xl);
    font-weight: var(--font-weight-bold);
    color: var(--color-text-primary);
    margin-bottom: var(--space-12);
  }

  .benefits-grid {
    display: grid;
    gap: var(--space-8);
    grid-template-columns: 1fr;
  }

  @media (min-width: 768px) {
    .benefits-grid {
      grid-template-columns: repeat(2, 1fr);
    }
  }

  .benefit-card {
    text-align: center;
    padding: var(--space-8);
    background: linear-gradient(135deg, var(--color-bg-secondary) 0%, var(--color-bg-tertiary) 100%);
    border: 1px solid var(--color-border);
    border-radius: var(--radius-lg);
    opacity: 0;
    transform: translateY(20px);
    animation: fadeInUp 0.6s ease-out calc(0.3s + var(--delay)) forwards;
  }

  @keyframes fadeInUp {
    to {
      opacity: 1;
      transform: translateY(0);
    }
  }

  .benefit-icon {
    font-size: 48px;
    margin-bottom: var(--space-4);
  }

  .benefit-title {
    font-size: var(--text-xl);
    font-weight: var(--font-weight-bold);
    color: var(--color-text-primary);
    margin-bottom: var(--space-3);
  }

  .benefit-description {
    font-size: var(--text-base);
    color: var(--color-text-secondary);
    line-height: var(--leading-relaxed);
  }
</style>