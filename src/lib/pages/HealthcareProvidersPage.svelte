<script>
  import { onMount } from 'svelte';

  let isVisible = $state(false);
  let sectionRef;

  const benefits = [
    {
      icon: '⚡',
      title: 'Same-Day Reimbursements',
      description: 'Get paid within 24 hours of claim submission with our automated processing system.'
    },
    {
      icon: '📱',
      title: 'Digital Claims Processing',
      description: 'Submit and track claims digitally through our web portal or mobile app.'
    },
    {
      icon: '✅',
      title: 'Instant Benefit Verification',
      description: 'Verify patient eligibility and coverage in real-time before providing services.'
    },
    {
      icon: '🏥',
      title: 'Comprehensive Network',
      description: 'Join 1,200+ healthcare providers serving 50,000+ covered employees.'
    },
    {
      icon: '📊',
      title: 'Analytics Dashboard',
      description: 'Track your performance, payment history, and patient demographics.'
    },
    {
      icon: '🛡️',
      title: 'Secure & Compliant',
      description: 'HIPAA-compliant platform with bank-level security and data protection.'
    }
  ];

  const steps = [
    {
      step: '01',
      title: 'Quick Registration',
      description: 'Complete our simple online registration form in just 15 minutes.',
      details: [
        'Basic practice information',
        'Medical licenses and certifications',
        'Banking details for payments',
        'Service offerings and specialties'
      ]
    },
    {
      step: '02',
      title: 'Verification Process',
      description: 'Our team verifies your credentials and approves your application within 2 business days.',
      details: [
        'License verification',
        'Accreditation checks',
        'Quality assurance review',
        'Network approval'
      ]
    },
    {
      step: '03',
      title: 'Platform Training',
      description: 'Get onboarded with comprehensive training on our platform and processes.',
      details: [
        'System walkthrough',
        'Claims submission training',
        'Best practices guide',
        'Dedicated support contact'
      ]
    },
    {
      step: '04',
      title: 'Start Serving Patients',
      description: 'Begin providing services to SimpleTPA members and receive fast payments.',
      details: [
        'Patient verification access',
        'Claims submission portal',
        'Real-time payment tracking',
        'Ongoing support'
      ]
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

<section bind:this={sectionRef} class="healthcare-providers">
  <!-- Hero Section -->
  <div class="hero-section section">
    <div class="container">
      <div class="hero-content" class:animate={isVisible}>
        <h1 class="hero-title">Join Our Healthcare Provider Network</h1>
        <p class="hero-description">
          Partner with SimpleTPA to serve more patients while enjoying same-day reimbursements, 
          digital claims processing, and comprehensive support for your practice.
        </p>
        <div class="hero-cta">
          <a href="/contact" class="btn-primary">
            Join Network Today
            <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <path d="M7 17L17 7" />
              <path d="M7 7h10v10" />
            </svg>
          </a>
          <a href="#benefits" class="btn-secondary">Learn More</a>
        </div>
      </div>
    </div>
  </div>

  <!-- Benefits Section -->
  <div id="benefits" class="benefits-section section">
    <div class="container">
      <h2 class="section-title text-center">Why Healthcare Providers Choose SimpleTPA</h2>
      
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

  <!-- Join Process -->
  <div class="process-section section">
    <div class="container">
      <h2 class="section-title text-center">Simple 4-Step Registration Process</h2>
      
      <div class="steps-container">
        {#each steps as step, index}
          <div class="step-card" style="--delay: {index * 0.2}s">
            <div class="step-number">{step.step}</div>
            <div class="step-content">
              <h3 class="step-title">{step.title}</h3>
              <p class="step-description">{step.description}</p>
              <ul class="step-details">
                {#each step.details as detail}
                  <li class="detail-item">
                    <svg class="detail-icon" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                      <path d="M20 6L9 17l-5-5"/>
                    </svg>
                    {detail}
                  </li>
                {/each}
              </ul>
            </div>
          </div>
        {/each}
      </div>
    </div>
  </div>

  <!-- Statistics -->
  <div class="stats-section section">
    <div class="container">
      <div class="stats-grid">
        <div class="stat-card">
          <div class="stat-number">1,200+</div>
          <div class="stat-label">Healthcare Providers</div>
          <div class="stat-description">Hospitals, clinics, and specialists in our network</div>
        </div>
        <div class="stat-card">
          <div class="stat-number">24 hrs</div>
          <div class="stat-label">Payment Processing</div>
          <div class="stat-description">Average time from claim to payment</div>
        </div>
        <div class="stat-card">
          <div class="stat-number">99.2%</div>
          <div class="stat-label">Approval Rate</div>
          <div class="stat-description">Claims approved on first submission</div>
        </div>
        <div class="stat-card">
          <div class="stat-number">50,000+</div>
          <div class="stat-label">Covered Lives</div>
          <div class="stat-description">Employees and dependents you can serve</div>
        </div>
      </div>
    </div>
  </div>

  <!-- CTA Section -->
  <div class="cta-section section">
    <div class="container">
      <div class="cta-content">
        <h2 class="cta-title">Ready to Transform Your Practice?</h2>
        <p class="cta-description">
          Join the SimpleTPA network today and start enjoying faster payments, 
          digital processes, and access to thousands of new patients.
        </p>
        <div class="cta-buttons">
          <a href="/contact" class="btn-primary">Start Registration</a>
        </div>
      </div>
    </div>
  </div>
</section>

<style>
  .healthcare-providers {
    padding-top: 0;
  }

  /* Hero Section */
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

  /* Benefits Section */
  .benefits-section {
    background-color: var(--color-bg-primary);
  }

  .section-title {
    font-size: var(--text-3xl);
    font-weight: var(--font-weight-bold);
    color: var(--color-text-primary);
    margin-bottom: var(--space-12);
  }

  @media (min-width: 768px) {
    .section-title {
      font-size: var(--text-4xl);
    }
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

  @media (min-width: 1024px) {
    .benefits-grid {
      grid-template-columns: repeat(3, 1fr);
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
    transition: all 0.3s ease-out;
  }

  .benefit-card:hover {
    transform: translateY(-4px);
    box-shadow: var(--shadow-lg);
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

  /* Process Section */
  .process-section {
    background: linear-gradient(180deg, var(--color-bg-primary) 0%, var(--color-bg-secondary) 100%);
  }

  .steps-container {
    display: grid;
    gap: var(--space-8);
    grid-template-columns: 1fr;
  }

  @media (min-width: 768px) {
    .steps-container {
      grid-template-columns: repeat(2, 1fr);
    }
  }

  .step-card {
    display: flex;
    gap: var(--space-6);
    padding: var(--space-8);
    background: linear-gradient(135deg, var(--color-bg-secondary) 0%, var(--color-bg-tertiary) 100%);
    border: 1px solid var(--color-border);
    border-radius: var(--radius-lg);
    opacity: 0;
    transform: translateX(-20px);
    animation: slideInLeft 0.6s ease-out calc(0.4s + var(--delay)) forwards;
  }

  @keyframes slideInLeft {
    to {
      opacity: 1;
      transform: translateX(0);
    }
  }

  .step-number {
    flex-shrink: 0;
    width: 48px;
    height: 48px;
    border-radius: 50%;
    background: linear-gradient(135deg, var(--color-accent) 0%, var(--color-accent-hover) 100%);
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: var(--text-lg);
    font-weight: var(--font-weight-bold);
    color: white;
  }

  .step-title {
    font-size: var(--text-xl);
    font-weight: var(--font-weight-bold);
    color: var(--color-text-primary);
    margin-bottom: var(--space-3);
  }

  .step-description {
    font-size: var(--text-base);
    color: var(--color-text-secondary);
    margin-bottom: var(--space-4);
  }

  .step-details {
    list-style: none;
    display: flex;
    flex-direction: column;
    gap: var(--space-2);
  }

  .detail-item {
    display: flex;
    align-items: center;
    gap: var(--space-2);
    font-size: var(--text-sm);
    color: var(--color-text-secondary);
  }

  .detail-icon {
    color: var(--color-success);
    flex-shrink: 0;
  }

  /* Stats Section */
  .stats-section {
    background-color: var(--color-bg-secondary);
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
    background: linear-gradient(135deg, var(--color-bg-primary) 0%, var(--color-bg-tertiary) 100%);
    border: 1px solid var(--color-border);
    border-radius: var(--radius-lg);
  }

  .stat-number {
    font-size: var(--text-3xl);
    font-weight: var(--font-weight-bold);
    color: var(--color-text-primary);
    line-height: var(--leading-none);
    margin-bottom: var(--space-2);
  }

  .stat-label {
    font-size: var(--text-base);
    font-weight: var(--font-weight-semibold);
    color: var(--color-accent);
    margin-bottom: var(--space-2);
  }

  .stat-description {
    font-size: var(--text-sm);
    color: var(--color-text-secondary);
  }

  /* CTA Section */
  .cta-section {
    background: linear-gradient(135deg, var(--color-bg-primary) 0%, var(--color-bg-secondary) 100%);
  }

  .cta-content {
    text-align: center;
    max-width: 600px;
    margin: 0 auto;
  }

  .cta-title {
    font-size: var(--text-3xl);
    font-weight: var(--font-weight-bold);
    color: var(--color-text-primary);
    margin-bottom: var(--space-4);
  }

  .cta-description {
    font-size: var(--text-lg);
    color: var(--color-text-secondary);
    margin-bottom: var(--space-8);
  }

  .cta-buttons {
    display: flex;
    flex-direction: column;
    gap: var(--space-4);
    align-items: center;
  }

  @media (min-width: 640px) {
    .cta-buttons {
      flex-direction: row;
      justify-content: center;
    }
  }
</style>