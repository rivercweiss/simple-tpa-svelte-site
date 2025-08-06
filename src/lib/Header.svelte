<script>
  let mobileMenuOpen = $state(false);
  let bannerVisible = $state(true);

  const navigation = [
    { name: 'About', href: '/about' },
    { name: 'How It Works', href: '/how-tpa-works' },
    { name: 'Providers', href: '/healthcare-providers' },
    { name: 'Corporations', href: '/sme-corporations' },
    { name: 'Network', href: '/provider-network' }
  ];

  function toggleMobileMenu() {
    mobileMenuOpen = !mobileMenuOpen;
  }

  function closeMobileMenu() {
    mobileMenuOpen = false;
  }

  function closeBanner() {
    bannerVisible = false;
  }
</script>

<header class="header">
  <!-- Member Portal Banner -->
  {#if bannerVisible}
    <div class="portal-banner">
      <div class="banner-container">
        <div class="banner-content">
          <div class="banner-text">
            <span class="banner-icon">🔐</span>
            <span class="banner-message">Access your benefits and claims</span>
          </div>
          <div class="banner-actions">
            <a href="https://app.simpletpa.com/member#?navSignature=0" target="_blank" rel="noopener noreferrer" class="portal-btn">
              Member Portal
              <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <path d="M7 17L17 7" />
                <path d="M7 7h10v10" />
              </svg>
            </a>
            <button onclick={closeBanner} class="close-btn" aria-label="Close banner">
              <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <path d="M18 6L6 18" />
                <path d="M6 6l12 12" />
              </svg>
            </button>
          </div>
        </div>
      </div>
    </div>
  {/if}

  <nav class="nav">
    <div class="nav-container">
      <!-- Logo -->
      <a href="/" class="logo" onclick={closeMobileMenu}>
        <img src="/SimpleTPA-logo-colored.webp" alt="SimpleTPA" class="logo-image" />
      </a>

      <!-- Desktop Navigation -->
      <div class="nav-links">
        {#each navigation as item}
          <a href={item.href} class="nav-link">{item.name}</a>
        {/each}
      </div>

      <!-- CTA Button -->
      <div class="nav-cta">
        <a href="/contact" class="contact-btn">
          Contact Us
          <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
            <line x1="22" y1="2" x2="11" y2="13"/>
            <polygon points="22,2 15,22 11,13 2,9"/>
          </svg>
        </a>
      </div>

      <!-- Mobile Menu Button -->
      <button class="mobile-menu-btn" onclick={toggleMobileMenu} aria-label="Toggle menu">
        <span class="hamburger" class:active={mobileMenuOpen}></span>
      </button>
    </div>

    <!-- Mobile Navigation -->
    {#if mobileMenuOpen}
      <div class="mobile-nav">
        <div class="mobile-nav-links">
          {#each navigation as item}
            <a href={item.href} class="mobile-nav-link" onclick={closeMobileMenu}>{item.name}</a>
          {/each}
          <a href="/contact" class="contact-btn mobile-cta" onclick={closeMobileMenu}>
            Get Started
            <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
              <line x1="22" y1="2" x2="11" y2="13"/>
              <polygon points="22,2 15,22 11,13 2,9"/>
            </svg>
          </a>
        </div>
      </div>
    {/if}
  </nav>
</header>

<style>
  .header {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    z-index: 50;
  }

  /* Portal Banner */
  .portal-banner {
    background: linear-gradient(135deg, var(--color-accent) 0%, var(--color-accent-hover) 100%);
    border-bottom: 1px solid rgba(255, 255, 255, 0.1);
  }

  .banner-container {
    max-width: var(--container-max-width);
    margin: 0 auto;
    padding: 0 var(--space-4);
  }

  @media (min-width: 768px) {
    .banner-container {
      padding: 0 var(--space-8);
    }
  }

  .banner-content {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: var(--space-3) 0;
    gap: var(--space-4);
  }

  .banner-text {
    display: flex;
    align-items: center;
    gap: var(--space-2);
    color: white;
  }

  .banner-icon {
    font-size: var(--text-base);
  }

  .banner-message {
    font-size: var(--text-sm);
    font-weight: var(--font-weight-medium);
  }

  @media (max-width: 640px) {
    .banner-message {
      display: none;
    }
  }

  .banner-actions {
    display: flex;
    align-items: center;
    gap: var(--space-3);
  }

  .portal-btn {
    display: inline-flex;
    align-items: center;
    gap: var(--space-2);
    padding: var(--space-2) var(--space-4);
    background: rgba(255, 255, 255, 0.15);
    color: white;
    text-decoration: none;
    border-radius: var(--radius);
    font-size: var(--text-sm);
    font-weight: var(--font-weight-medium);
    transition: all var(--transition-fast);
    backdrop-filter: blur(10px);
  }

  .portal-btn:hover {
    background: rgba(255, 255, 255, 0.2);
    color: white;
    transform: translateY(-1px);
  }

  .close-btn {
    background: none;
    border: none;
    color: rgba(255, 255, 255, 0.8);
    cursor: pointer;
    padding: var(--space-2);
    border-radius: var(--radius-sm);
    transition: all var(--transition-fast);
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .close-btn:hover {
    background: rgba(255, 255, 255, 0.1);
    color: white;
  }

  /* Navigation */
  .nav {
    background-color: rgba(255, 255, 255, 0.95);
    backdrop-filter: blur(20px);
    border-bottom: 1px solid rgba(0, 0, 0, 0.08);
    height: 64px;
  }

  .nav-container {
    display: flex;
    align-items: center;
    justify-content: space-between;
    height: 100%;
    max-width: var(--container-max-width);
    margin: 0 auto;
    padding: 0 var(--space-6);
  }

  @media (min-width: 768px) {
    .nav-container {
      padding: 0 var(--space-8);
    }
  }

  /* Logo */
  .logo {
    display: flex;
    align-items: center;
    text-decoration: none;
    z-index: 1;
  }

  .logo-image {
    height: 32px;
    width: auto;
    max-width: 140px;
  }

  /* Desktop Navigation */
  .nav-links {
    display: none;
    align-items: center;
    gap: var(--space-6);
    margin-left: var(--space-12);
    margin-right: var(--space-12);
  }

  @media (min-width: 1024px) {
    .nav-links {
      display: flex;
    }
  }

  .nav-link {
    font-size: var(--text-sm);
    font-weight: var(--font-weight-medium);
    color: var(--color-text-secondary);
    text-decoration: none;
    transition: all var(--transition-fast);
    padding: var(--space-2) var(--space-3);
    border-radius: var(--radius);
    letter-spacing: -0.01em;
    white-space: nowrap;
  }

  .nav-link:hover {
    color: var(--color-text-primary);
    background-color: var(--color-bg-secondary);
  }

  /* Contact Button - Send Message Style */
  .nav-cta {
    display: none;
  }

  @media (min-width: 1024px) {
    .nav-cta {
      display: block;
    }
  }

  .contact-btn {
    display: inline-flex;
    align-items: center;
    gap: var(--space-2);
    padding: var(--space-3) var(--space-6);
    background: linear-gradient(135deg, var(--color-accent) 0%, #7983d8 100%);
    color: white;
    text-decoration: none;
    border-radius: var(--radius-md);
    font-size: var(--text-sm);
    font-weight: var(--font-weight-medium);
    transition: all var(--transition-fast);
    box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
    letter-spacing: -0.01em;
  }

  .contact-btn:hover {
    transform: translateY(-1px);
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
    background: linear-gradient(135deg, var(--color-accent-hover) 0%, #6b73d8 100%);
    color: white;
  }

  .contact-btn svg {
    transition: transform var(--transition-fast);
  }

  .contact-btn:hover svg {
    transform: translateX(1px);
  }

  /* Mobile Menu Button */
  .mobile-menu-btn {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 32px;
    height: 32px;
    background: none;
    border: none;
    cursor: pointer;
    padding: 0;
    z-index: 2;
  }

  @media (min-width: 1024px) {
    .mobile-menu-btn {
      display: none;
    }
  }

  .hamburger {
    position: relative;
    width: 18px;
    height: 2px;
    background-color: var(--color-text-primary);
    transition: all var(--transition-fast);
    border-radius: 1px;
  }

  .hamburger::before,
  .hamburger::after {
    content: '';
    position: absolute;
    width: 18px;
    height: 2px;
    background-color: var(--color-text-primary);
    transition: all var(--transition-fast);
    border-radius: 1px;
  }

  .hamburger::before {
    top: -6px;
  }

  .hamburger::after {
    top: 6px;
  }

  .hamburger.active {
    background-color: transparent;
  }

  .hamburger.active::before {
    top: 0;
    transform: rotate(45deg);
  }

  .hamburger.active::after {
    top: 0;
    transform: rotate(-45deg);
  }

  /* Mobile Navigation */
  .mobile-nav {
    position: absolute;
    top: 100%;
    left: 0;
    right: 0;
    background-color: rgba(255, 255, 255, 0.98);
    backdrop-filter: blur(20px);
    border-bottom: 1px solid rgba(0, 0, 0, 0.08);
    animation: fadeIn 0.2s ease-out;
  }

  @media (min-width: 1024px) {
    .mobile-nav {
      display: none;
    }
  }

  .mobile-nav-links {
    display: flex;
    flex-direction: column;
    padding: var(--space-6);
    gap: var(--space-2);
  }

  .mobile-nav-link {
    display: block;
    padding: var(--space-3);
    font-size: var(--text-base);
    font-weight: var(--font-weight-medium);
    color: var(--color-text-secondary);
    text-decoration: none;
    transition: all var(--transition-fast);
    border-radius: var(--radius);
    letter-spacing: -0.01em;
  }

  .mobile-nav-link:hover {
    color: var(--color-text-primary);
    background-color: var(--color-bg-secondary);
  }

  .mobile-cta {
    margin-top: var(--space-6);
    text-align: center;
    justify-content: center;
  }
</style>