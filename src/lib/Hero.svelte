<script>
  import { onMount } from 'svelte';

  let heroRef;
  let isVisible = $state(false);

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

    if (heroRef) {
      observer.observe(heroRef);
    }

    return () => {
      if (heroRef) {
        observer.unobserve(heroRef);
      }
    };
  });
</script>

<section bind:this={heroRef} class="hero">
  <div class="hero-container">
    <div class="hero-content" class:animate={isVisible}>
      <div class="hero-badge">
        <span class="badge-text">🏥 Trusted by Healthcare Leaders</span>
      </div>
      
      <h1 class="hero-title">
        Streamline Healthcare
        <span class="gradient-text">Administration</span>
      </h1>
      
      <p class="hero-description">
        Save 30% or more on healthcare costs while improving patient care. 
        Our digital platform connects companies, employees, and healthcare providers seamlessly.
      </p>
      
      <div class="hero-cta">
        <a href="/contact" class="btn-primary">
          Get Started Today
          <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <path d="M7 17L17 7" />
            <path d="M7 7h10v10" />
          </svg>
        </a>
        <a href="/how-tpa-works" class="btn-secondary">
          Learn How It Works
        </a>
      </div>
      
      <div class="hero-stats">
        <div class="stat">
          <div class="stat-number">30%+</div>
          <div class="stat-label">Cost Savings</div>
        </div>
        <div class="stat">
          <div class="stat-number">15min</div>
          <div class="stat-label">Provider Registration</div>
        </div>
        <div class="stat">
          <div class="stat-number">Same Day</div>
          <div class="stat-label">Reimbursements</div>
        </div>
      </div>
    </div>
    
    <div class="hero-visual" class:animate={isVisible}>
      <div class="visual-container">
        <div class="dashboard-mockup">
          <div class="mockup-header">
            <div class="mockup-dots">
              <div class="dot"></div>
              <div class="dot"></div>
              <div class="dot"></div>
            </div>
            <div class="mockup-title">SimpleTPA Dashboard</div>
          </div>
          <div class="mockup-content">
            <div class="mockup-card">
              <div class="card-header">
                <div class="card-icon health"></div>
                <div class="card-title">Cost Savings</div>
              </div>
              <div class="card-value">30%+</div>
              <div class="card-trend positive">vs traditional insurance</div>
            </div>
            <div class="mockup-card">
              <div class="card-header">
                <div class="card-icon time"></div>
                <div class="card-title">Payment Processing</div>
              </div>
              <div class="card-value">Same Day</div>
              <div class="card-trend positive">Instant reimbursement</div>
            </div>
            <div class="mockup-card">
              <div class="card-header">
                <div class="card-icon users"></div>
                <div class="card-title">Provider Network</div>
              </div>
              <div class="card-value">20+</div>
              <div class="card-trend positive">Leading hospitals</div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>

<style>
  .hero {
    position: relative;
    min-height: fit-content;
    padding-top: 5%;
    padding-bottom: 5%;
    display: flex;
    align-items: center;
    background: linear-gradient(180deg, var(--color-bg-primary) 0%, var(--color-bg-secondary) 100%);
  }

  .hero-container {
    max-width: var(--container-max-width);
    margin: 0 auto;
    padding: 0 var(--space-4);
    display: grid;
    gap: var(--space-12);
    align-items: center;
    grid-template-columns: 1fr;
  }

  @media (min-width: 768px) {
    .hero-container {
      padding: 0 var(--space-8);
      gap: var(--space-16);
    }
  }

  @media (min-width: 1024px) {
    .hero-container {
      grid-template-columns: 1fr 1fr;
    }
  }

  /* Hero Content */
  .hero-content {
    display: flex;
    flex-direction: column;
    gap: var(--space-6);
    opacity: 0;
    transform: translateY(30px);
    transition: all 0.8s ease-out;
  }

  .hero-content.animate {
    opacity: 1;
    transform: translateY(0);
  }

  .hero-badge {
    display: inline-flex;
    align-self: flex-start;
  }

  .badge-text {
    padding: var(--space-2) var(--space-4);
    background: linear-gradient(135deg, var(--color-bg-secondary) 0%, var(--color-bg-tertiary) 100%);
    border: 1px solid var(--color-border);
    border-radius: var(--radius-xl);
    font-size: var(--text-sm);
    font-weight: var(--font-weight-medium);
    color: var(--color-text-secondary);
  }

  .hero-title {
    font-size: var(--text-4xl);
    font-weight: var(--font-weight-bold);
    line-height: var(--leading-tight);
    color: var(--color-text-primary);
    letter-spacing: -0.02em;
  }

  @media (min-width: 768px) {
    .hero-title {
      font-size: var(--text-5xl);
    }
  }

  @media (min-width: 1024px) {
    .hero-title {
      font-size: var(--text-6xl);
    }
  }

  .hero-description {
    font-size: var(--text-lg);
    line-height: var(--leading-relaxed);
    color: var(--color-text-secondary);
    max-width: 500px;
  }

  /* CTA Buttons */
  .hero-cta {
    display: flex;
    flex-direction: column;
    gap: var(--space-4);
  }

  @media (min-width: 640px) {
    .hero-cta {
      flex-direction: row;
    }
  }

  /* Hero Stats */
  .hero-stats {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: var(--space-6);
    margin-top: var(--space-8);
  }

  .stat {
    text-align: center;
  }

  @media (min-width: 1024px) {
    .stat {
      text-align: left;
    }
  }

  .stat-number {
    font-size: var(--text-2xl);
    font-weight: var(--font-weight-bold);
    color: var(--color-text-primary);
    line-height: var(--leading-none);
  }

  .stat-label {
    font-size: var(--text-sm);
    font-weight: var(--font-weight-medium);
    color: var(--color-text-tertiary);
    margin-top: var(--space-1);
  }

  /* Hero Visual */
  .hero-visual {
    display: none;
    opacity: 0;
    transform: translateY(30px) scale(0.95);
    transition: all 0.8s ease-out 0.2s;
  }

  .hero-visual.animate {
    opacity: 1;
    transform: translateY(0) scale(1);
  }

  @media (min-width: 1024px) {
    .hero-visual {
      display: block;
    }
  }

  /* Dashboard Mockup */
  .dashboard-mockup {
    background: linear-gradient(135deg, var(--color-bg-secondary) 0%, var(--color-bg-tertiary) 100%);
    border: 1px solid var(--color-border);
    border-radius: var(--radius-lg);
    overflow: hidden;
    box-shadow: var(--shadow-lg);
  }

  .mockup-header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: var(--space-4);
    border-bottom: 1px solid var(--color-border);
  }

  .mockup-dots {
    display: flex;
    gap: var(--space-2);
  }

  .dot {
    width: 8px;
    height: 8px;
    border-radius: 50%;
    background-color: var(--color-text-tertiary);
  }

  .mockup-title {
    font-size: var(--text-sm);
    font-weight: var(--font-weight-medium);
    color: var(--color-text-secondary);
  }

  .mockup-content {
    padding: var(--space-6);
    display: flex;
    flex-direction: column;
    gap: var(--space-4);
  }

  .mockup-card {
    background: var(--color-bg-primary);
    border: 1px solid var(--color-border);
    border-radius: var(--radius);
    padding: var(--space-4);
  }

  .card-header {
    display: flex;
    align-items: center;
    gap: var(--space-3);
    margin-bottom: var(--space-3);
  }

  .card-icon {
    width: 24px;
    height: 24px;
    border-radius: var(--radius-sm);
  }

  .card-icon.health {
    background: linear-gradient(135deg, var(--color-success) 0%, #00b570 100%);
  }

  .card-icon.time {
    background: linear-gradient(135deg, var(--color-accent) 0%, var(--color-accent-hover) 100%);
  }

  .card-icon.users {
    background: linear-gradient(135deg, #f59e0b 0%, #d97706 100%);
  }

  .card-title {
    font-size: var(--text-sm);
    font-weight: var(--font-weight-medium);
    color: var(--color-text-secondary);
  }

  .card-value {
    font-size: var(--text-xl);
    font-weight: var(--font-weight-bold);
    color: var(--color-text-primary);
    margin-bottom: var(--space-2);
  }

  .card-trend {
    font-size: var(--text-xs);
    font-weight: var(--font-weight-medium);
  }

  .card-trend.positive {
    color: var(--color-success);
  }
</style>