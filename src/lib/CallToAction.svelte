<script>
  import { onMount } from 'svelte';

  let sectionRef;
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

<section bind:this={sectionRef} class="cta-section section">
  <div class="container">
    <div class="cta-content" class:animate={isVisible}>
      <div class="cta-badge">
        <span class="badge-text">⚡ Ready to Transform Healthcare?</span>
      </div>
      
      <h2 class="cta-title">
        Start Saving on Healthcare 
        <span class="gradient-text">Today</span>
      </h2>
      
      <p class="cta-description">
        Join leading healthcare providers who trust SimpleTPA to streamline their 
        healthcare administration and reduce costs by 30% or more.
      </p>
      
      <div class="cta-buttons">
        <a href="/contact" class="btn-primary cta-primary">
          Contact Us Today
          <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <path d="M7 17L17 7" />
            <path d="M7 7h10v10" />
          </svg>
        </a>
        <a href="/how-tpa-works" class="btn-secondary cta-secondary">
          Learn More
        </a>
      </div>
      
      <div class="cta-features">
        <div class="feature">
          <svg class="feature-icon" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <path d="M22 11.08V12a10 10 0 1 1-5.93-9.14"/>
            <path d="M9 11l3 3L22 4"/>
          </svg>
          <span class="feature-text">15-minute setup</span>
        </div>
        <div class="feature">
          <svg class="feature-icon" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <path d="M9 12l2 2 4-4"/>
            <circle cx="12" cy="12" r="10"/>
          </svg>
          <span class="feature-text">No setup fees</span>
        </div>
        <div class="feature">
          <svg class="feature-icon" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <path d="M16 21v-2a4 4 0 0 0-4-4H5a4 4 0 0 0-4 4v2"/>
            <circle cx="8.5" cy="7" r="4"/>
            <path d="M20 8v6M23 11h-6"/>
          </svg>
          <span class="feature-text">Dedicated support</span>
        </div>
      </div>
    </div>
  </div>
</section>

<style>
  .cta-section {
    background: var(--color-bg-secondary);
  }

  .cta-content {
    text-align: center;
    max-width: 800px;
    margin: 0 auto;
    opacity: 0;
    transform: translateY(30px);
    transition: all 0.8s ease-out;
  }

  .cta-content.animate {
    opacity: 1;
    transform: translateY(0);
  }

  .cta-badge {
    display: inline-flex;
    margin-bottom: var(--space-6);
  }

  .badge-text {
    padding: var(--space-2) var(--space-4);
    background: linear-gradient(135deg, var(--color-bg-secondary) 0%, var(--color-bg-tertiary) 100%);
    border: 1px solid var(--color-border);
    border-radius: var(--radius-xl);
    font-size: var(--text-sm);
    font-weight: var(--font-weight-medium);
    color: var(--color-text-secondary);
    animation: pulse-border 3s infinite;
  }

  @keyframes pulse-border {
    0%, 100% {
      border-color: var(--color-border);
      box-shadow: 0 0 0 0 rgba(94, 106, 210, 0);
    }
    50% {
      border-color: var(--color-accent);
      box-shadow: 0 0 0 4px rgba(94, 106, 210, 0.1);
    }
  }

  .cta-title {
    font-size: var(--text-4xl);
    font-weight: var(--font-weight-bold);
    color: var(--color-text-primary);
    line-height: var(--leading-tight);
    margin-bottom: var(--space-6);
    letter-spacing: -0.02em;
  }

  @media (min-width: 768px) {
    .cta-title {
      font-size: var(--text-5xl);
    }
  }

  .cta-description {
    font-size: var(--text-lg);
    color: var(--color-text-secondary);
    line-height: var(--leading-relaxed);
    margin-bottom: var(--space-8);
    max-width: 600px;
    margin-left: auto;
    margin-right: auto;
  }

  .cta-buttons {
    display: flex;
    flex-direction: column;
    gap: var(--space-4);
    margin-bottom: var(--space-12);
    align-items: center;
  }

  @media (min-width: 640px) {
    .cta-buttons {
      flex-direction: row;
      justify-content: center;
    }
  }

  .cta-primary {
    position: relative;
    overflow: hidden;
    transition: all 0.3s ease-out;
  }

  .cta-primary::before {
    content: '';
    position: absolute;
    top: 0;
    left: -100%;
    width: 100%;
    height: 100%;
    background: linear-gradient(90deg, transparent, rgba(255, 255, 255, 0.1), transparent);
    transition: left 0.5s;
  }

  .cta-primary:hover::before {
    left: 100%;
  }

  .cta-primary:hover {
    transform: translateY(-2px);
    box-shadow: 
      0 10px 40px rgba(94, 106, 210, 0.3),
      0 0 0 1px rgba(94, 106, 210, 0.1);
  }

  .cta-secondary {
    transition: all 0.3s ease-out;
  }

  .cta-secondary:hover {
    transform: translateY(-2px);
    box-shadow: var(--shadow);
  }

  .cta-features {
    display: flex;
    flex-direction: column;
    gap: var(--space-4);
    justify-content: center;
    align-items: center;
  }

  @media (min-width: 640px) {
    .cta-features {
      flex-direction: row;
      gap: var(--space-8);
    }
  }

  .feature {
    display: flex;
    align-items: center;
    gap: var(--space-2);
  }

  .feature-icon {
    color: var(--color-success);
    flex-shrink: 0;
  }

  .feature-text {
    font-size: var(--text-sm);
    font-weight: var(--font-weight-medium);
    color: var(--color-text-secondary);
  }

  /* Enhanced button animations */
  .btn-primary,
  .btn-secondary {
    position: relative;
    transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  }

  .btn-primary:hover {
    transform: translateY(-2px) scale(1.02);
  }

  .btn-secondary:hover {
    transform: translateY(-1px);
  }

  .btn-primary:active {
    transform: translateY(0) scale(1);
  }

  .btn-secondary:active {
    transform: translateY(0);
  }
</style>