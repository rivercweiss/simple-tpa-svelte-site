<script>
  let isVisible = $state(true);

  function closeBanner() {
    isVisible = false;
  }
</script>

{#if isVisible}
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

<style>
  .portal-banner {
    background: linear-gradient(135deg, var(--color-accent) 0%, var(--color-accent-hover) 100%);
    border-bottom: 1px solid rgba(255, 255, 255, 0.1);
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    z-index: 60;
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
</style>