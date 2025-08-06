<script>
  import ContactForm from '../ContactForm.svelte';
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

<section bind:this={sectionRef} class="contact-page">
  <!-- Hero Section -->
  <div class="hero-section section">
    <div class="container">
      <div class="hero-content" class:animate={isVisible}>
        <h1 class="hero-title">Contact SimpleTPA</h1>
        <p class="hero-description">
          Ready to transform your healthcare administration? Get in touch with our team 
          to learn how SimpleTPA can help you save costs and streamline operations.
        </p>
      </div>
    </div>
  </div>

  <!-- Contact Form -->
  <ContactForm />

  <!-- Contact Information -->
  <div class="contact-info-section section">
    <div class="container">
      <div class="contact-info-grid">
        <div class="info-card">
          <div class="card-icon">
            <svg width="32" height="32" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <path d="M21 10c0 7-9 13-9 13s-9-6-9-13a9 9 0 0 1 18 0z"/>
              <circle cx="12" cy="10" r="3"/>
            </svg>
          </div>
          <h3 class="card-title">Visit Our Office</h3>
          <p class="card-description">
            7th Floor, Unit B, 8Rockwell<br>
            Hidalgo Drive, Rockwell Center<br>
            Makati, 1210, Philippines
          </p>
        </div>

        <div class="info-card">
          <div class="card-icon">
            <svg width="32" height="32" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <path d="M22 16.92v3a2 2 0 0 1-2.18 2 19.79 19.79 0 0 1-8.63-3.07 19.5 19.5 0 0 1-6-6 19.79 19.79 0 0 1-3.07-8.67A2 2 0 0 1 4.11 2h3a2 2 0 0 1 2 1.72 12.84 12.84 0 0 0 .7 2.81 2 2 0 0 1-.45 2.11L8.09 9.91a16 16 0 0 0 6 6l1.27-1.27a2 2 0 0 1 2.11-.45 12.84 12.84 0 0 0 2.81.7A2 2 0 0 1 22 16.92z"/>
            </svg>
          </div>
          <h3 class="card-title">Call Us</h3>
          <p class="card-description">
            <a href="tel:+639088928375" class="contact-link">+63 (908) 892 8375</a><br>
            Monday - Friday: 9AM - 6PM
          </p>
        </div>

        <div class="info-card">
          <div class="card-icon">
            <svg width="32" height="32" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/>
              <polyline points="22,6 12,13 2,6"/>
            </svg>
          </div>
          <h3 class="card-title">Email Us</h3>
          <p class="card-description">
            <a href="mailto:contactus@simpletpa.com" class="contact-link">contactus@simpletpa.com</a><br>
            We'll respond within 24 hours
          </p>
        </div>
      </div>
    </div>
  </div>
</section>

<style>
  .contact-page {
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
  }

  /* Contact Info Section */
  .contact-info-section {
    background-color: var(--color-bg-primary);
  }

  .contact-info-grid {
    display: grid;
    gap: var(--space-8);
    grid-template-columns: 1fr;
  }

  @media (min-width: 1024px) {
    .contact-info-grid {
      grid-template-columns: repeat(3, 1fr);
    }
  }

  .info-card {
    text-align: center;
    padding: var(--space-8);
    background: linear-gradient(135deg, var(--color-bg-secondary) 0%, var(--color-bg-tertiary) 100%);
    border: 1px solid var(--color-border);
    border-radius: var(--radius-lg);
    transition: all 0.3s ease-out;
  }

  .info-card:hover {
    transform: translateY(-4px);
    box-shadow: var(--shadow-lg);
  }

  .card-icon {
    color: var(--color-accent);
    margin-bottom: var(--space-4);
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
  }

  .contact-link {
    color: var(--color-accent);
    text-decoration: none;
    transition: color var(--transition-fast);
  }

  .contact-link:hover {
    color: var(--color-accent-hover);
  }
</style>