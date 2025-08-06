<script>
  import { onMount } from 'svelte';

  let sectionRef;
  let isVisible = $state(false);

  const providers = [
    { name: 'De La Salle Medical Center', logo: '/images/DLSMC-Logo-300x300.png' },
    { name: 'St. Luke\'s Medical Center - QC', logo: '/images/SLMC-QC-Logo.png' },
    { name: 'St. Luke\'s Medical Center - GC', logo: '/images/SLMC-GC-Logo.jpeg' },
    { name: 'Philippine General Medical Center', logo: '/images/PGMC-Logo-2010.jpg' },
    { name: 'Fe Del Mundo Hospital', logo: '/images/Fe-Del-Mundo-Hospital.jpeg' },
    { name: 'Cardinal Medical Center', logo: '/images/CMC_RCRH-Logo-New-300x150.png' },
    { name: 'Tagaytay Medical Center', logo: '/images/Tagaytay-Med-Logo.png' },
    { name: 'San Miguel Medical Center', logo: '/images/SMMC-Logo.jpeg' }
  ];

  const testimonials = [
    {
      quote: "SimpleTPA helped us save over 30% on healthcare costs while providing better benefits to our employees. The cashless system eliminates paperwork and speeds up everything.",
      author: "Maria Santos",
      title: "HR Director",
      company: "Philippine Tech Corp"
    },
    {
      quote: "The 15-minute provider registration and same-day payment processing make SimpleTPA incredibly efficient. Our patients get instant coverage approval.",
      author: "Dr. Juan Dela Cruz",
      title: "Chief Medical Officer",
      company: "Metro Medical Network"
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

<section bind:this={sectionRef} class="social-proof section">
  <div class="container">
    <!-- Provider Network -->
    <div class="providers-section" class:animate={isVisible}>
      <div class="section-header">
        <h2 class="section-title">Trusted by Leading Healthcare Providers</h2>
        <p class="section-description">
          Leading healthcare providers across the Philippines trust SimpleTPA 
          for seamless benefit administration and same-day reimbursements.
        </p>
      </div>

      <div class="providers-grid">
        {#each providers as provider, index}
          <div class="provider-card" style="--delay: {index * 0.1}s">
            <div class="provider-logo">
              <img src={provider.logo} alt={provider.name} class="provider-image" />
            </div>
            <div class="provider-name">{provider.name}</div>
          </div>
        {/each}
      </div>
    </div>

    <!-- Statistics -->
    <div class="stats-section" class:animate={isVisible}>
      <div class="stats-grid">
        <div class="stat-card">
          <div class="stat-icon">💰</div>
          <div class="stat-number">30%+</div>
          <div class="stat-label">Healthcare Cost Savings</div>
        </div>
        <div class="stat-card">
          <div class="stat-icon">⚡</div>
          <div class="stat-number">Same-day</div>
          <div class="stat-label">Payment Processing</div>
        </div>
        <div class="stat-card">
          <div class="stat-icon">🏥</div>
          <div class="stat-number">20+</div>
          <div class="stat-label">Healthcare Providers</div>
        </div>
        <div class="stat-card">
          <div class="stat-icon">👥</div>
          <div class="stat-number">118+</div>
          <div class="stat-label">Years Combined Experience</div>
        </div>
      </div>
    </div>

    <!-- Testimonials -->
    <div class="testimonials-section" class:animate={isVisible}>
      <div class="section-header">
        <h2 class="section-title">What Our Clients Say</h2>
      </div>

      <div class="testimonials-grid">
        {#each testimonials as testimonial, index}
          <div class="testimonial-card" style="--delay: {index * 0.2}s">
            <div class="testimonial-content">
              <div class="quote-icon">
                <svg width="24" height="24" viewBox="0 0 24 24" fill="none">
                  <path d="M14.017 21v-7.391c0-5.704 3.731-9.57 8.983-10.609l.995 2.151c-2.432.917-3.995 3.638-3.995 5.849h4v10h-9.983zm-14.017 0v-7.391c0-5.704 3.748-9.57 9-10.609l.996 2.151c-2.433.917-3.996 3.638-3.996 5.849h3.983v10h-9.983z" fill="currentColor"/>
                </svg>
              </div>
              <blockquote class="testimonial-quote">
                "{testimonial.quote}"
              </blockquote>
            </div>
            <div class="testimonial-author">
              <div class="author-avatar">
                <span class="author-initial">{testimonial.author.charAt(0)}</span>
              </div>
              <div class="author-info">
                <div class="author-name">{testimonial.author}</div>
                <div class="author-title">{testimonial.title}</div>
                <div class="author-company">{testimonial.company}</div>
              </div>
            </div>
          </div>
        {/each}
      </div>
    </div>
  </div>
</section>

<style>
  .social-proof {
    background-color: var(--color-bg-primary);
  }

  /* Section Header */
  .section-header {
    text-align: center;
    margin-bottom: var(--space-16);
    opacity: 0;
    transform: translateY(20px);
    transition: all 0.6s ease-out;
  }

  .providers-section.animate .section-header,
  .testimonials-section.animate .section-header {
    opacity: 1;
    transform: translateY(0);
  }

  .section-title {
    font-size: var(--text-3xl);
    font-weight: var(--font-weight-bold);
    color: var(--color-text-primary);
    margin-bottom: var(--space-4);
  }

  @media (min-width: 768px) {
    .section-title {
      font-size: var(--text-4xl);
    }
  }

  .section-description {
    font-size: var(--text-lg);
    color: var(--color-text-secondary);
    max-width: 600px;
    margin: 0 auto;
    line-height: var(--leading-relaxed);
  }

  /* Provider Network */
  .providers-section {
    margin-bottom: var(--space-24);
  }

  .providers-grid {
    display: grid;
    gap: var(--space-6);
    grid-template-columns: repeat(2, 1fr);
  }

  @media (min-width: 640px) {
    .providers-grid {
      grid-template-columns: repeat(3, 1fr);
    }
  }

  @media (min-width: 1024px) {
    .providers-grid {
      grid-template-columns: repeat(4, 1fr);
    }
  }

  .provider-card {
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
    padding: var(--space-6);
    background: var(--color-bg-secondary);
    border: 1px solid var(--color-border);
    border-radius: var(--radius-lg);
    transition: all 0.3s ease-out;
    opacity: 0;
    transform: translateY(20px);
    animation: fadeInUp 0.5s ease-out calc(0.3s + var(--delay)) forwards;
  }

  .provider-card:hover {
    transform: translateY(-2px);
    border-color: var(--color-accent);
  }

  @keyframes fadeInUp {
    to {
      opacity: 1;
      transform: translateY(0);
    }
  }

  .provider-logo {
    width: 80px;
    height: 80px;
    border-radius: var(--radius);
    background: white;
    display: flex;
    align-items: center;
    justify-content: center;
    margin-bottom: var(--space-3);
    padding: var(--space-2);
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  }

  .provider-image {
    width: 100%;
    height: 100%;
    object-fit: contain;
    border-radius: var(--radius-sm);
  }

  .provider-name {
    font-size: var(--text-sm);
    font-weight: var(--font-weight-medium);
    color: var(--color-text-secondary);
    line-height: var(--leading-snug);
  }

  /* Statistics */
  .stats-section {
    margin-bottom: var(--space-24);
  }

  .stats-grid {
    display: grid;
    gap: var(--space-6);
    grid-template-columns: repeat(2, 1fr);
  }

  @media (min-width: 1024px) {
    .stats-grid {
      grid-template-columns: repeat(4, 1fr);
    }
  }

  .stat-card {
    text-align: center;
    padding: var(--space-8);
    background: linear-gradient(135deg, var(--color-bg-secondary) 0%, var(--color-bg-tertiary) 100%);
    border: 1px solid var(--color-border);
    border-radius: var(--radius-lg);
    transition: all 0.3s ease-out;
  }

  .stat-card:hover {
    transform: translateY(-2px);
    box-shadow: var(--shadow);
  }

  .stat-icon {
    font-size: 32px;
    margin-bottom: var(--space-3);
  }

  .stat-number {
    font-size: var(--text-3xl);
    font-weight: var(--font-weight-bold);
    color: var(--color-text-primary);
    line-height: var(--leading-none);
    margin-bottom: var(--space-2);
  }

  .stat-label {
    font-size: var(--text-sm);
    color: var(--color-text-secondary);
    font-weight: var(--font-weight-medium);
  }

  /* Testimonials */
  .testimonials-grid {
    display: grid;
    gap: var(--space-8);
    grid-template-columns: 1fr;
  }

  @media (min-width: 1024px) {
    .testimonials-grid {
      grid-template-columns: repeat(2, 1fr);
    }
  }

  .testimonial-card {
    background: linear-gradient(135deg, var(--color-bg-secondary) 0%, var(--color-bg-tertiary) 100%);
    border: 1px solid var(--color-border);
    border-radius: var(--radius-lg);
    padding: var(--space-8);
    opacity: 0;
    transform: translateY(20px);
    animation: fadeInUp 0.6s ease-out calc(0.5s + var(--delay)) forwards;
  }

  .testimonial-content {
    margin-bottom: var(--space-6);
  }

  .quote-icon {
    color: var(--color-accent);
    margin-bottom: var(--space-4);
  }

  .testimonial-quote {
    font-size: var(--text-lg);
    line-height: var(--leading-relaxed);
    color: var(--color-text-secondary);
    font-style: italic;
    margin: 0;
  }

  .testimonial-author {
    display: flex;
    align-items: center;
    gap: var(--space-4);
  }

  .author-avatar {
    width: 48px;
    height: 48px;
    border-radius: 50%;
    background: linear-gradient(135deg, var(--color-accent) 0%, var(--color-accent-hover) 100%);
    display: flex;
    align-items: center;
    justify-content: center;
    flex-shrink: 0;
  }

  .author-initial {
    font-size: var(--text-lg);
    font-weight: var(--font-weight-bold);
    color: white;
  }

  .author-name {
    font-size: var(--text-base);
    font-weight: var(--font-weight-semibold);
    color: var(--color-text-primary);
  }

  .author-title {
    font-size: var(--text-sm);
    color: var(--color-text-secondary);
  }

  .author-company {
    font-size: var(--text-sm);
    color: var(--color-text-tertiary);
  }
</style>