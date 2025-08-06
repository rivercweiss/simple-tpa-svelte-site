<script>
  const currentYear = new Date().getFullYear();

  const footerLinks = {
    company: [
      { name: 'About', href: '/about' },
      { name: 'How TPA Works', href: '/how-tpa-works' },
      { name: 'Careers', href: '/careers' },
      { name: 'Contact', href: '/contact' }
    ],
    services: [
      { name: 'Healthcare Providers', href: '/healthcare-providers' },
      { name: 'SMEs & Corporations', href: '/sme-corporations' },
      { name: 'Provider Network', href: '/provider-network' }
    ],
    legal: [
      { name: 'Privacy Policy', href: '/privacy-policy' },
      { name: 'Terms & Conditions', href: '/terms-conditions' },
      { name: 'Anti-Corruption Policy', href: '/anti-corruption-policy' }
    ]
  };
</script>

<footer class="footer">
  <div class="footer-container">
    <div class="footer-content">
      <!-- Company Info -->
      <div class="footer-section">
        <div class="footer-logo">
          <span class="logo-simple">SIMPLE</span><span class="logo-tpa">TPA</span>
        </div>
        <p class="footer-description">
          Streamlining healthcare administration and saving companies 30% or more on healthcare costs through innovative technology solutions.
        </p>
        <div class="footer-contact">
          <div class="contact-item">
            <span class="contact-label">Email:</span>
            <a href="mailto:contactus@simpletpa.com" class="contact-link">contactus@simpletpa.com</a>
          </div>
          <div class="contact-item">
            <span class="contact-label">Phone:</span>
            <a href="tel:+639088928375" class="contact-link">+63 (908) 892 8375</a>
          </div>
          <div class="contact-item">
            <span class="contact-label">Address:</span>
            <span class="contact-text">7th Floor, Unit B, 8Rockwell, Hidalgo Drive, Rockwell Center, Makati, 1210, Philippines</span>
          </div>
        </div>
      </div>

      <!-- Company Links -->
      <div class="footer-section">
        <h4 class="footer-title">Company</h4>
        <ul class="footer-links">
          {#each footerLinks.company as link}
            <li>
              <a href={link.href} class="footer-link">{link.name}</a>
            </li>
          {/each}
        </ul>
      </div>

      <!-- Services Links -->
      <div class="footer-section">
        <h4 class="footer-title">Services</h4>
        <ul class="footer-links">
          {#each footerLinks.services as link}
            <li>
              <a href={link.href} class="footer-link">{link.name}</a>
            </li>
          {/each}
        </ul>
      </div>

      <!-- Legal Links -->
      <div class="footer-section">
        <h4 class="footer-title">Legal</h4>
        <ul class="footer-links">
          {#each footerLinks.legal as link}
            <li>
              <a href={link.href} class="footer-link">{link.name}</a>
            </li>
          {/each}
        </ul>
      </div>
    </div>

    <!-- Footer Bottom -->
    <div class="footer-bottom">
      <div class="footer-bottom-content">
        <p class="copyright">
          © {currentYear} SimpleTPA. All rights reserved.
        </p>
        <p class="tagline">
          Simplifying Healthcare Administration
        </p>
      </div>
    </div>
  </div>
</footer>

<style>
  .footer {
    background-color: var(--color-bg-secondary);
    border-top: 1px solid var(--color-border);
  }

  .footer-container {
    max-width: var(--container-max-width);
    margin: 0 auto;
    padding: var(--space-16) var(--space-4) var(--space-8);
  }

  @media (min-width: 768px) {
    .footer-container {
      padding: var(--space-24) var(--space-8) var(--space-12);
    }
  }

  .footer-content {
    display: grid;
    gap: var(--space-8);
    grid-template-columns: repeat(1, 1fr);
  }

  @media (min-width: 768px) {
    .footer-content {
      grid-template-columns: repeat(2, 1fr);
    }
  }

  @media (min-width: 1024px) {
    .footer-content {
      grid-template-columns: 2fr 1fr 1fr 1fr;
      gap: var(--space-12);
    }
  }

  /* Footer Section */
  .footer-section {
    display: flex;
    flex-direction: column;
    gap: var(--space-4);
  }

  /* Logo */
  .footer-logo {
    font-weight: var(--font-weight-bold);
    font-size: var(--text-xl);
    margin-bottom: var(--space-2);
  }

  .logo-simple {
    color: var(--color-text-primary);
  }

  .logo-tpa {
    color: var(--color-accent);
  }

  /* Description */
  .footer-description {
    font-size: var(--text-sm);
    line-height: var(--leading-relaxed);
    color: var(--color-text-secondary);
    margin-bottom: var(--space-4);
  }

  /* Contact Info */
  .footer-contact {
    display: flex;
    flex-direction: column;
    gap: var(--space-2);
  }

  .contact-item {
    display: flex;
    flex-direction: column;
    gap: var(--space-1);
  }

  @media (min-width: 768px) {
    .contact-item {
      flex-direction: row;
      align-items: center;
    }
  }

  .contact-label {
    font-size: var(--text-sm);
    font-weight: var(--font-weight-medium);
    color: var(--color-text-tertiary);
    min-width: 60px;
  }

  .contact-link {
    font-size: var(--text-sm);
    color: var(--color-text-secondary);
    text-decoration: none;
    transition: color var(--transition-fast);
  }

  .contact-link:hover {
    color: var(--color-accent);
  }

  .contact-text {
    font-size: var(--text-sm);
    color: var(--color-text-secondary);
    line-height: var(--leading-relaxed);
  }

  /* Footer Title */
  .footer-title {
    font-size: var(--text-base);
    font-weight: var(--font-weight-semibold);
    color: var(--color-text-primary);
    margin-bottom: var(--space-2);
  }

  /* Footer Links */
  .footer-links {
    list-style: none;
    display: flex;
    flex-direction: column;
    gap: var(--space-3);
  }

  .footer-link {
    font-size: var(--text-sm);
    color: var(--color-text-secondary);
    text-decoration: none;
    transition: color var(--transition-fast);
  }

  .footer-link:hover {
    color: var(--color-text-primary);
  }

  /* Footer Bottom */
  .footer-bottom {
    margin-top: var(--space-12);
    padding-top: var(--space-8);
    border-top: 1px solid var(--color-border);
  }

  .footer-bottom-content {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: var(--space-2);
    text-align: center;
  }

  @media (min-width: 768px) {
    .footer-bottom-content {
      flex-direction: row;
      justify-content: space-between;
      text-align: left;
    }
  }

  .copyright {
    font-size: var(--text-sm);
    color: var(--color-text-tertiary);
  }

  .tagline {
    font-size: var(--text-sm);
    color: var(--color-text-tertiary);
    font-style: italic;
  }
</style>