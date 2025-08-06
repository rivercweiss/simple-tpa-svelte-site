<script>
  import { onMount } from 'svelte';

  let isVisible = $state(false);
  let activeStep = $state(1);
  let sectionRef;

  const steps = [
    {
      id: 1,
      title: 'Registration & Setup',
      subtitle: 'Get started in minutes',
      description: 'Companies register with SimpleTPA and set up their healthcare benefit plans. Our team provides full onboarding support to ensure smooth integration with existing systems.',
      features: [
        'Quick 15-minute online registration',
        'Dedicated account manager assigned',
        'Custom benefit plan configuration',
        'Employee enrollment assistance'
      ],
      icon: '📝'
    },
    {
      id: 2,
      title: 'Employee Enrollment',
      subtitle: 'Simple for employees',
      description: 'Employees receive their digital healthcare cards and can immediately access the provider network. Our user-friendly platform makes enrollment effortless.',
      features: [
        'Digital healthcare ID cards',
        'Mobile app access',
        'Instant benefit verification',
        'Real-time provider directory'
      ],
      icon: '👥'
    },
    {
      id: 3,
      title: 'Healthcare Service',
      subtitle: 'Seamless care delivery',
      description: 'Employees visit any healthcare provider in our network. Providers verify benefits instantly and provide necessary care without upfront payments from patients.',
      features: [
        'Instant benefit verification',
        'Cashless transactions',
        'Real-time eligibility checks',
        'Comprehensive provider network'
      ],
      icon: '🏥'
    },
    {
      id: 4,
      title: 'Claims Processing',
      subtitle: 'Lightning-fast processing',
      description: 'Claims are processed automatically through our intelligent system. Providers receive same-day reimbursements, and companies get real-time cost tracking.',
      features: [
        'Automated claims processing',
        'Same-day reimbursements',
        'Real-time cost tracking',
        'Detailed reporting and analytics'
      ],
      icon: '⚡'
    }
  ];

  const benefits = [
    {
      category: 'For Employers',
      items: [
        { title: '30% Cost Reduction', description: 'Average savings on healthcare administration costs' },
        { title: 'Reduced HR Workload', description: 'Automated processes eliminate manual paperwork' },
        { title: 'Real-time Analytics', description: 'Comprehensive dashboards and reporting' },
        { title: 'Compliance Management', description: 'Automatic regulatory compliance tracking' }
      ]
    },
    {
      category: 'For Employees',
      items: [
        { title: 'Easy Access', description: 'Mobile app and web portal for benefit management' },
        { title: 'Wide Network', description: '20+ leading healthcare providers' },
        { title: 'Cashless Transactions', description: 'No upfront payments required' },
        { title: 'Real-time Updates', description: 'Instant claim status and benefit tracking' }
      ]
    },
    {
      category: 'For Providers',
      items: [
        { title: 'Same-day Payments', description: 'Fastest reimbursement in the industry' },
        { title: 'Digital Processing', description: 'Paperless claims and benefit verification' },
        { title: 'Instant Verification', description: 'Real-time patient eligibility checks' },
        { title: 'Dedicated Support', description: '24/7 technical and administrative support' }
      ]
    }
  ];

  function setActiveStep(stepId) {
    activeStep = stepId;
  }

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

<section bind:this={sectionRef} class="how-tpa-works">
  <!-- Hero Section -->
  <div class="hero-section section">
    <div class="container">
      <div class="hero-content" class:animate={isVisible}>
        <h1 class="hero-title">How SimpleTPA Works</h1>
        <p class="hero-description">
          Our platform simplifies healthcare administration through a seamless 4-step process 
          that connects employers, employees, and healthcare providers.
        </p>
      </div>
    </div>
  </div>

  <!-- Process Steps -->
  <div class="process-section section">
    <div class="container">
      <h2 class="section-title text-center">Simple 4-Step Process</h2>
      
      <!-- Step Navigation -->
      <div class="step-navigation">
        {#each steps as step}
          <button 
            class="step-nav-button"
            class:active={activeStep === step.id}
            onclick={() => setActiveStep(step.id)}
          >
            <div class="step-number">{step.id}</div>
            <div class="step-nav-content">
              <div class="step-nav-title">{step.title}</div>
              <div class="step-nav-subtitle">{step.subtitle}</div>
            </div>
          </button>
        {/each}
      </div>

      <!-- Active Step Content -->
      {#each steps as step}
        {#if activeStep === step.id}
          <div class="step-content" key={step.id}>
            <div class="step-visual">
              <div class="step-icon">{step.icon}</div>
              <div class="step-progress">
                <div class="progress-bar">
                  <div class="progress-fill" style="width: {(step.id / steps.length) * 100}%"></div>
                </div>
                <div class="progress-text">Step {step.id} of {steps.length}</div>
              </div>
            </div>
            
            <div class="step-details">
              <h3 class="step-title">{step.title}</h3>
              <p class="step-description">{step.description}</p>
              
              <div class="step-features">
                <h4 class="features-title">Key Features:</h4>
                <ul class="features-list">
                  {#each step.features as feature}
                    <li class="feature-item">
                      <svg class="feature-icon" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                        <path d="M20 6L9 17l-5-5"/>
                      </svg>
                      {feature}
                    </li>
                  {/each}
                </ul>
              </div>
            </div>
          </div>
        {/if}
      {/each}
    </div>
  </div>

  <!-- Benefits Section -->
  <div class="benefits-section section">
    <div class="container">
      <h2 class="section-title text-center">Benefits for Everyone</h2>
      
      <div class="benefits-grid">
        {#each benefits as benefitGroup, index}
          <div class="benefit-group" style="--delay: {index * 0.2}s">
            <h3 class="benefit-category">{benefitGroup.category}</h3>
            <div class="benefit-items">
              {#each benefitGroup.items as item}
                <div class="benefit-item">
                  <div class="benefit-title">{item.title}</div>
                  <div class="benefit-description">{item.description}</div>
                </div>
              {/each}
            </div>
          </div>
        {/each}
      </div>
    </div>
  </div>

  <!-- Technology Features -->
  <div class="technology-section section">
    <div class="container">
      <div class="technology-content">
        <div class="tech-text">
          <h2 class="tech-title">Powered by Advanced Technology</h2>
          <p class="tech-description">
            Our platform leverages cutting-edge technology to deliver fast, reliable, 
            and secure healthcare administration services.
          </p>
          
          <div class="tech-features">
            <div class="tech-feature">
              <div class="tech-feature-icon">🔒</div>
              <div class="tech-feature-content">
                <div class="tech-feature-title">Bank-level Security</div>
                <div class="tech-feature-description">256-bit encryption and HIPAA compliance</div>
              </div>
            </div>
            
            <div class="tech-feature">
              <div class="tech-feature-icon">⚡</div>
              <div class="tech-feature-content">
                <div class="tech-feature-title">Real-time Processing</div>
                <div class="tech-feature-description">Instant benefit verification and claims processing</div>
              </div>
            </div>
            
            <div class="tech-feature">
              <div class="tech-feature-icon">📱</div>
              <div class="tech-feature-content">
                <div class="tech-feature-title">Mobile-first Design</div>
                <div class="tech-feature-description">Responsive web and native mobile applications</div>
              </div>
            </div>
            
            <div class="tech-feature">
              <div class="tech-feature-icon">🔄</div>
              <div class="tech-feature-content">
                <div class="tech-feature-title">Seamless Integration</div>
                <div class="tech-feature-description">API-first architecture for easy system integration</div>
              </div>
            </div>
          </div>
        </div>
        
        <div class="tech-visual">
          <div class="tech-dashboard">
            <div class="dashboard-header">
              <div class="header-title">SimpleTPA Platform</div>
              <div class="header-status">
                <span class="status-dot active"></span>
                <span class="status-text">Live</span>
              </div>
            </div>
            <div class="dashboard-content">
              <div class="dashboard-metric">
                <div class="metric-label">Payment Processing</div>
                <div class="metric-value">Same Day</div>
                <div class="metric-trend positive">Instant reimbursement</div>
              </div>
              <div class="dashboard-metric">
                <div class="metric-label">Cost Savings</div>
                <div class="metric-value">30%+</div>
                <div class="metric-trend positive">vs traditional insurance</div>
              </div>
              <div class="dashboard-metric">
                <div class="metric-label">Provider Network</div>
                <div class="metric-value">20+</div>
                <div class="metric-trend positive">Leading hospitals</div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>

<style>
  .how-tpa-works {
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

  /* Process Section */
  .process-section {
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

  /* Step Navigation */
  .step-navigation {
    display: grid;
    gap: var(--space-4);
    grid-template-columns: 1fr;
    margin-bottom: var(--space-12);
  }

  @media (min-width: 768px) {
    .step-navigation {
      grid-template-columns: repeat(2, 1fr);
    }
  }

  @media (min-width: 1024px) {
    .step-navigation {
      grid-template-columns: repeat(4, 1fr);
    }
  }

  .step-nav-button {
    display: flex;
    align-items: center;
    gap: var(--space-4);
    padding: var(--space-4);
    background: var(--color-bg-secondary);
    border: 1px solid var(--color-border);
    border-radius: var(--radius-lg);
    color: var(--color-text-secondary);
    cursor: pointer;
    transition: all 0.2s ease-out;
    text-align: left;
    width: 100%;
  }

  .step-nav-button:hover {
    background: var(--color-bg-tertiary);
    border-color: var(--color-accent);
    transform: translateY(-1px);
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  }

  .step-nav-button.active {
    background: linear-gradient(135deg, var(--color-accent) 0%, var(--color-accent-hover) 100%);
    border-color: var(--color-accent);
    color: white;
    transform: translateY(-2px);
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
  }

  .step-nav-button.active:hover {
    transform: translateY(-2px);
    box-shadow: 0 6px 16px rgba(0, 0, 0, 0.2);
  }

  .step-number {
    width: 32px;
    height: 32px;
    border-radius: 50%;
    background: var(--color-bg-primary);
    display: flex;
    align-items: center;
    justify-content: center;
    font-weight: var(--font-weight-bold);
    font-size: var(--text-sm);
    flex-shrink: 0;
    transition: all 0.2s ease-out;
  }

  .step-nav-button:hover .step-number {
    background: var(--color-accent);
    color: white;
  }

  .step-nav-button.active .step-number {
    background: rgba(255, 255, 255, 0.2);
    color: white;
  }

  .step-nav-title {
    font-size: var(--text-base);
    font-weight: var(--font-weight-semibold);
    margin-bottom: var(--space-1);
  }

  .step-nav-subtitle {
    font-size: var(--text-sm);
    opacity: 0.8;
  }

  /* Step Content */
  .step-content {
    display: grid;
    gap: var(--space-8);
    grid-template-columns: 1fr;
    align-items: center;
    animation: fadeIn 0.5s ease-out;
  }

  @media (min-width: 1024px) {
    .step-content {
      grid-template-columns: 1fr 2fr;
    }
  }

  @keyframes fadeIn {
    from {
      opacity: 0;
      transform: translateY(20px);
    }
    to {
      opacity: 1;
      transform: translateY(0);
    }
  }

  .step-visual {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: var(--space-6);
  }

  .step-icon {
    font-size: 80px;
    margin-bottom: var(--space-4);
  }

  .step-progress {
    width: 100%;
    max-width: 200px;
  }

  .progress-bar {
    width: 100%;
    height: 4px;
    background: var(--color-border);
    border-radius: 2px;
    overflow: hidden;
    margin-bottom: var(--space-2);
  }

  .progress-fill {
    height: 100%;
    background: linear-gradient(90deg, var(--color-accent) 0%, var(--color-success) 100%);
    border-radius: 2px;
    transition: width 0.5s ease-out;
  }

  .progress-text {
    text-align: center;
    font-size: var(--text-sm);
    color: var(--color-text-tertiary);
  }

  .step-details {
    text-align: center;
  }

  @media (min-width: 1024px) {
    .step-details {
      text-align: left;
    }
  }

  .step-title {
    font-size: var(--text-2xl);
    font-weight: var(--font-weight-bold);
    color: var(--color-text-primary);
    margin-bottom: var(--space-4);
  }

  .step-description {
    font-size: var(--text-base);
    color: var(--color-text-secondary);
    line-height: var(--leading-relaxed);
    margin-bottom: var(--space-6);
  }

  .features-title {
    font-size: var(--text-lg);
    font-weight: var(--font-weight-semibold);
    color: var(--color-text-primary);
    margin-bottom: var(--space-4);
  }

  .features-list {
    list-style: none;
    display: flex;
    flex-direction: column;
    gap: var(--space-3);
  }

  .feature-item {
    display: flex;
    align-items: center;
    gap: var(--space-3);
    font-size: var(--text-sm);
    color: var(--color-text-secondary);
  }

  .feature-icon {
    color: var(--color-success);
    flex-shrink: 0;
  }

  /* Benefits Section */
  .benefits-section {
    background: linear-gradient(180deg, var(--color-bg-primary) 0%, var(--color-bg-secondary) 100%);
  }

  .benefits-grid {
    display: grid;
    gap: var(--space-8);
    grid-template-columns: 1fr;
  }

  @media (min-width: 1024px) {
    .benefits-grid {
      grid-template-columns: repeat(3, 1fr);
    }
  }

  .benefit-group {
    background: linear-gradient(135deg, var(--color-bg-secondary) 0%, var(--color-bg-tertiary) 100%);
    border: 1px solid var(--color-border);
    border-radius: var(--radius-lg);
    padding: var(--space-8);
    opacity: 0;
    transform: translateY(20px);
    animation: fadeInUp 0.6s ease-out calc(0.3s + var(--delay)) forwards;
  }

  @keyframes fadeInUp {
    to {
      opacity: 1;
      transform: translateY(0);
    }
  }

  .benefit-category {
    font-size: var(--text-xl);
    font-weight: var(--font-weight-bold);
    color: var(--color-text-primary);
    margin-bottom: var(--space-6);
    text-align: center;
  }

  .benefit-items {
    display: flex;
    flex-direction: column;
    gap: var(--space-4);
  }

  .benefit-item {
    padding: var(--space-4);
    background: var(--color-bg-primary);
    border: 1px solid var(--color-border);
    border-radius: var(--radius);
  }

  .benefit-title {
    font-size: var(--text-base);
    font-weight: var(--font-weight-semibold);
    color: var(--color-text-primary);
    margin-bottom: var(--space-2);
  }

  .benefit-description {
    font-size: var(--text-sm);
    color: var(--color-text-secondary);
    line-height: var(--leading-relaxed);
  }

  /* Technology Section */
  .technology-section {
    background-color: var(--color-bg-secondary);
  }

  .technology-content {
    display: grid;
    gap: var(--space-12);
    grid-template-columns: 1fr;
    align-items: center;
  }

  @media (min-width: 1024px) {
    .technology-content {
      grid-template-columns: 1fr 1fr;
    }
  }

  .tech-title {
    font-size: var(--text-3xl);
    font-weight: var(--font-weight-bold);
    color: var(--color-text-primary);
    margin-bottom: var(--space-4);
  }

  .tech-description {
    font-size: var(--text-lg);
    color: var(--color-text-secondary);
    line-height: var(--leading-relaxed);
    margin-bottom: var(--space-8);
  }

  .tech-features {
    display: flex;
    flex-direction: column;
    gap: var(--space-6);
  }

  .tech-feature {
    display: flex;
    gap: var(--space-4);
    align-items: flex-start;
  }

  .tech-feature-icon {
    font-size: 24px;
    flex-shrink: 0;
  }

  .tech-feature-title {
    font-size: var(--text-base);
    font-weight: var(--font-weight-semibold);
    color: var(--color-text-primary);
    margin-bottom: var(--space-1);
  }

  .tech-feature-description {
    font-size: var(--text-sm);
    color: var(--color-text-secondary);
  }

  /* Tech Dashboard */
  .tech-dashboard {
    background: linear-gradient(135deg, var(--color-bg-primary) 0%, var(--color-bg-tertiary) 100%);
    border: 1px solid var(--color-border);
    border-radius: var(--radius-lg);
    overflow: hidden;
    box-shadow: var(--shadow-lg);
  }

  .dashboard-header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: var(--space-4);
    border-bottom: 1px solid var(--color-border);
    background: var(--color-bg-secondary);
  }

  .header-title {
    font-size: var(--text-base);
    font-weight: var(--font-weight-medium);
    color: var(--color-text-primary);
  }

  .header-status {
    display: flex;
    align-items: center;
    gap: var(--space-2);
  }

  .status-dot {
    width: 8px;
    height: 8px;
    border-radius: 50%;
    background: var(--color-success);
    animation: pulse 2s infinite;
  }

  @keyframes pulse {
    0%, 100% {
      opacity: 1;
    }
    50% {
      opacity: 0.5;
    }
  }

  .status-text {
    font-size: var(--text-sm);
    color: var(--color-success);
    font-weight: var(--font-weight-medium);
  }

  .dashboard-content {
    padding: var(--space-6);
    display: flex;
    flex-direction: column;
    gap: var(--space-6);
  }

  .dashboard-metric {
    text-align: center;
  }

  .metric-label {
    font-size: var(--text-sm);
    color: var(--color-text-tertiary);
    margin-bottom: var(--space-2);
  }

  .metric-value {
    font-size: var(--text-2xl);
    font-weight: var(--font-weight-bold);
    color: var(--color-text-primary);
    margin-bottom: var(--space-1);
  }

  .metric-trend {
    font-size: var(--text-xs);
    font-weight: var(--font-weight-medium);
  }

  .metric-trend.positive {
    color: var(--color-success);
  }
</style>