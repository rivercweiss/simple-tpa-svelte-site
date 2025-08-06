<script>
  import { onMount } from 'svelte';

  let isVisible = $state(false);
  let sectionRef;

  const providers = [
    { name: 'De La Salle Medical Center', logo: '/images/DLSMC-Logo-300x300.png', location: 'Dasmariñas, Cavite', specialty: 'Multi-specialty Hospital' },
    { name: 'St. Luke\'s Medical Center - QC', logo: '/images/SLMC-QC-Logo.png', location: 'Quezon City', specialty: 'Multi-specialty Hospital' },
    { name: 'St. Luke\'s Medical Center - GC', logo: '/images/SLMC-GC-Logo.jpeg', location: 'Bonifacio Global City', specialty: 'Multi-specialty Hospital' },
    { name: 'Philippine General Medical Center', logo: '/images/PGMC-Logo-2010.jpg', location: 'Manila', specialty: 'Government Hospital' },
    { name: 'Fe Del Mundo Hospital', logo: '/images/Fe-Del-Mundo-Hospital.jpeg', location: 'Quezon City', specialty: 'Children\'s Hospital' },
    { name: 'Cardinal Medical Center', logo: '/images/CMC_RCRH-Logo-New-300x150.png', location: 'San Juan', specialty: 'Multi-specialty Hospital' },
    { name: 'Tagaytay Medical Center', logo: '/images/Tagaytay-Med-Logo.png', location: 'Tagaytay', specialty: 'Multi-specialty Hospital' },
    { name: 'San Miguel Medical Center', logo: '/images/SMMC-Logo.jpeg', location: 'San Miguel', specialty: 'Multi-specialty Hospital' }
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

<section bind:this={sectionRef} class="provider-network">
  <!-- Hero Section -->
  <div class="hero-section section">
    <div class="container">
      <div class="hero-content" class:animate={isVisible}>
        <h1 class="hero-title">Our Provider Network</h1>
        <p class="hero-description">
          Access to leading healthcare providers across the Philippines, 
          including multi-specialty hospitals, clinics, and specialist centers.
        </p>
      </div>
    </div>
  </div>

  <!-- Network Stats -->
  <div class="stats-section section">
    <div class="container">
      <div class="stats-grid">
        <div class="stat-card">
          <div class="stat-number">20+</div>
          <div class="stat-label">Healthcare Providers</div>
        </div>
        <div class="stat-card">
          <div class="stat-number">15min</div>
          <div class="stat-label">Provider Registration</div>
        </div>
        <div class="stat-card">
          <div class="stat-number">Same Day</div>
          <div class="stat-label">Reimbursements</div>
        </div>
      </div>
    </div>
  </div>

  <!-- Provider List -->
  <div class="providers-section section">
    <div class="container">
      <h2 class="section-title text-center">Featured Healthcare Providers</h2>
      
      <div class="providers-grid">
        {#each providers as provider, index}
          <div class="provider-card" style="--delay: {index * 0.1}s">
            <div class="provider-logo">
              <img src={provider.logo} alt={provider.name} class="provider-image" />
            </div>
            <div class="provider-info">
              <h3 class="provider-name">{provider.name}</h3>
              <div class="provider-location">{provider.location}</div>
              <div class="provider-specialty">{provider.specialty}</div>
            </div>
          </div>
        {/each}
      </div>
    </div>
  </div>
</section>

<style>
  .provider-network {
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
  }

  .stats-section {
    background-color: var(--color-bg-primary);
  }

  .stats-grid {
    display: grid;
    gap: var(--space-6);
    grid-template-columns: 1fr;
  }

  @media (min-width: 640px) {
    .stats-grid {
      grid-template-columns: repeat(3, 1fr);
    }
  }

  .stat-card {
    text-align: center;
    padding: var(--space-6);
    background: linear-gradient(135deg, var(--color-bg-secondary) 0%, var(--color-bg-tertiary) 100%);
    border: 1px solid var(--color-border);
    border-radius: var(--radius-lg);
  }

  .stat-number {
    font-size: var(--text-2xl);
    font-weight: var(--font-weight-bold);
    color: var(--color-text-primary);
    margin-bottom: var(--space-2);
  }

  .stat-label {
    font-size: var(--text-sm);
    color: var(--color-text-secondary);
  }

  .providers-section {
    background: linear-gradient(180deg, var(--color-bg-primary) 0%, var(--color-bg-secondary) 100%);
  }

  .section-title {
    font-size: var(--text-3xl);
    font-weight: var(--font-weight-bold);
    color: var(--color-text-primary);
    margin-bottom: var(--space-12);
  }

  .providers-grid {
    display: grid;
    gap: var(--space-6);
    grid-template-columns: 1fr;
  }

  @media (min-width: 768px) {
    .providers-grid {
      grid-template-columns: repeat(2, 1fr);
    }
  }

  @media (min-width: 1024px) {
    .providers-grid {
      grid-template-columns: repeat(3, 1fr);
    }
  }

  .provider-card {
    display: flex;
    gap: var(--space-4);
    padding: var(--space-6);
    background: linear-gradient(135deg, var(--color-bg-secondary) 0%, var(--color-bg-tertiary) 100%);
    border: 1px solid var(--color-border);
    border-radius: var(--radius-lg);
    opacity: 0;
    transform: translateY(20px);
    animation: fadeInUp 0.5s ease-out calc(0.3s + var(--delay)) forwards;
    transition: all 0.3s ease-out;
  }

  .provider-card:hover {
    transform: translateY(-2px);
    box-shadow: var(--shadow);
  }

  @keyframes fadeInUp {
    to {
      opacity: 1;
      transform: translateY(0);
    }
  }

  .provider-logo {
    width: 64px;
    height: 64px;
    border-radius: var(--radius);
    background: white;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-shrink: 0;
    padding: var(--space-2);
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
    border: 1px solid var(--color-border);
  }

  .provider-image {
    width: 100%;
    height: 100%;
    object-fit: contain;
    border-radius: var(--radius-sm);
  }

  .provider-name {
    font-size: var(--text-base);
    font-weight: var(--font-weight-semibold);
    color: var(--color-text-primary);
    margin-bottom: var(--space-2);
  }

  .provider-location {
    font-size: var(--text-sm);
    color: var(--color-text-secondary);
    margin-bottom: var(--space-1);
  }

  .provider-specialty {
    font-size: var(--text-xs);
    color: var(--color-text-tertiary);
  }
</style>