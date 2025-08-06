<script>
  import { onMount } from 'svelte';

  let sectionRef;
  let isVisible = $state(false);

  const propositions = [
    {
      icon: '🏢',
      title: 'For Employers',
      description: 'Reduce HR administrative workload and lower healthcare costs by 30% or more with our streamlined digital platform.',
      features: [
        'Automated benefit management',
        'Real-time cost tracking',
        'Employee self-service portal',
        'Comprehensive reporting'
      ],
      cta: 'Learn More',
      href: '/sme-corporations'
    },
    {
      icon: '🏥',
      title: 'For Healthcare Providers',
      description: 'Join our network and enjoy instant registration, same-day reimbursements, and seamless patient benefit verification.',
      features: [
        '15-minute registration process',
        'Same-day reimbursements',
        'Digital claims processing',
        'Patient benefit verification'
      ],
      cta: 'Join Network',
      href: '/healthcare-providers'
    },
    {
      icon: '👥',
      title: 'For Employees',
      description: 'Access your healthcare benefits easily with our user-friendly platform and extensive provider network.',
      features: [
        'Instant coverage verification',
        'Cashless healthcare access',
        '24/7 telemedicine services',
        'Mobile-friendly platform'
      ],
      cta: 'Get Started',
      href: '/contact'
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

<section bind:this={sectionRef} class="value-propositions section">
  <div class="container">
    <div class="section-header" class:animate={isVisible}>
      <h2 class="section-title">
        Built for Everyone in Healthcare
      </h2>
      <p class="section-description">
        Our platform connects all stakeholders in the healthcare ecosystem, 
        providing tailored solutions for employers, healthcare providers, and employees.
      </p>
    </div>

    <div class="propositions-grid" class:animate={isVisible}>
      {#each propositions as proposition, index}
        <div class="proposition-card" style="--delay: {index * 0.1}s">
          <div class="card-icon">
            <span class="icon-emoji">{proposition.icon}</span>
          </div>
          
          <div class="card-content">
            <h3 class="card-title">{proposition.title}</h3>
            <p class="card-description">{proposition.description}</p>
            
            <ul class="card-features">
              {#each proposition.features as feature}
                <li class="feature-item">
                  <svg class="feature-icon" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                    <path d="M20 6L9 17l-5-5"/>
                  </svg>
                  <span class="feature-text">{feature}</span>
                </li>
              {/each}
            </ul>
          </div>

          <div class="card-footer">
            <a href={proposition.href} class="card-cta">
              {proposition.cta}
              <svg class="cta-icon" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <path d="M7 17L17 7" />
                <path d="M7 7h10v10" />
              </svg>
            </a>
          </div>
        </div>
      {/each}
    </div>
  </div>
</section>

<style>
  .value-propositions {
    background: linear-gradient(180deg, var(--color-bg-primary) 0%, var(--color-bg-secondary) 100%);
  }

  /* Section Header */
  .section-header {
    text-align: center;
    margin-bottom: var(--space-16);
    opacity: 0;
    transform: translateY(20px);
    transition: all 0.6s ease-out;
  }

  .section-header.animate {
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

  /* Propositions Grid */
  .propositions-grid {
    display: grid;
    gap: var(--space-8);
    grid-template-columns: 1fr;
  }

  @media (min-width: 768px) {
    .propositions-grid {
      grid-template-columns: repeat(2, 1fr);
    }
  }

  @media (min-width: 1024px) {
    .propositions-grid {
      grid-template-columns: repeat(3, 1fr);
    }
  }

  .propositions-grid.animate .proposition-card {
    opacity: 1;
    transform: translateY(0);
  }

  /* Proposition Card */
  .proposition-card {
    background: linear-gradient(135deg, var(--color-bg-secondary) 0%, var(--color-bg-tertiary) 100%);
    border: 1px solid var(--color-border);
    border-radius: var(--radius-lg);
    padding: var(--space-8);
    display: flex;
    flex-direction: column;
    height: 100%;
    transition: all 0.3s ease-out;
    opacity: 0;
    transform: translateY(30px);
    animation: fadeInUp 0.6s ease-out calc(0.2s + var(--delay)) forwards;
    position: relative;
    overflow: hidden;
  }

  .proposition-card::before {
    content: '';
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    height: 2px;
    background: linear-gradient(90deg, var(--color-accent) 0%, var(--color-success) 100%);
    transform: scaleX(0);
    transition: transform 0.3s ease-out;
  }

  .proposition-card:hover {
    transform: translateY(-4px);
    box-shadow: var(--shadow-lg);
    border-color: var(--color-accent);
  }

  .proposition-card:hover::before {
    transform: scaleX(1);
  }

  @keyframes fadeInUp {
    to {
      opacity: 1;
      transform: translateY(0);
    }
  }

  /* Card Icon */
  .card-icon {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 60px;
    height: 60px;
    border-radius: var(--radius-lg);
    background: linear-gradient(135deg, var(--color-bg-primary) 0%, var(--color-bg-secondary) 100%);
    border: 1px solid var(--color-border);
    margin-bottom: var(--space-6);
  }

  .icon-emoji {
    font-size: 24px;
  }

  /* Card Content */
  .card-content {
    flex: 1;
    margin-bottom: var(--space-6);
  }

  .card-title {
    font-size: var(--text-xl);
    font-weight: var(--font-weight-bold);
    color: var(--color-text-primary);
    margin-bottom: var(--space-3);
  }

  .card-description {
    font-size: var(--text-base);
    color: var(--color-text-secondary);
    line-height: var(--leading-relaxed);
    margin-bottom: var(--space-6);
  }

  /* Features List */
  .card-features {
    list-style: none;
    display: flex;
    flex-direction: column;
    gap: var(--space-3);
  }

  .feature-item {
    display: flex;
    align-items: center;
    gap: var(--space-3);
  }

  .feature-icon {
    color: var(--color-success);
    flex-shrink: 0;
  }

  .feature-text {
    font-size: var(--text-sm);
    color: var(--color-text-secondary);
  }

  /* Card Footer */
  .card-footer {
    margin-top: auto;
  }

  .card-cta {
    display: inline-flex;
    align-items: center;
    gap: var(--space-2);
    font-size: var(--text-base);
    font-weight: var(--font-weight-medium);
    color: var(--color-accent);
    text-decoration: none;
    transition: all var(--transition-fast);
  }

  .card-cta:hover {
    color: var(--color-accent-hover);
    transform: translateX(2px);
  }

  .cta-icon {
    transition: transform var(--transition-fast);
  }

  .card-cta:hover .cta-icon {
    transform: rotate(45deg);
  }
</style>