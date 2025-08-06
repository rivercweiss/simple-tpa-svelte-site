<script>
  import { onMount } from 'svelte';

  let isVisible = $state(false);
  let sectionRef;

  const milestones = [
    { year: '2020', title: 'Company Founded', description: 'SimpleTPA was established with a vision to revolutionize healthcare administration in the Philippines.' },
    { year: '2021', title: 'First 100 Providers', description: 'Reached our first milestone of 100 healthcare providers on the platform.' },
    { year: '2022', title: 'Digital Innovation', description: 'Launched advanced digital tools for real-time benefit verification and claims processing.' },
    { year: '2023', title: '1000+ Providers', description: 'Expanded network to over 1,000 healthcare providers nationwide.' },
    { year: '2024', title: 'Major Partnerships', description: 'Formed strategic partnerships with leading corporations and medical centers.' }
  ];

  const team = [
    {
      name: 'Barry Clark',
      role: 'Co-Founder & Visionary',
      description: '53+ years of experience in building new markets for life & health insurers like AIG, ING, HSBC & Pacific Cross across Asia-Pacific.',
      initial: 'BC'
    },
    {
      name: 'Lee Wood',
      role: 'Co-Founder & President',
      description: '25 years of experience creating employee benefit programs and delivering business solutions for major financial institutions.',
      initial: 'LW'
    },
    {
      name: 'Anthony Doropan',
      role: 'Chief Technology Officer',
      description: '17 years of experience delivering technical solutions and healthcare system innovations for leading organizations.',
      initial: 'AD'
    },
    {
      name: 'Erwin Go',
      role: 'Marketing & Sales',
      description: '25 years of experience in marketing and sales for insurance and healthcare benefit programs across the Philippines.',
      initial: 'EG'
    }
  ];

  const values = [
    {
      icon: '🎯',
      title: 'Innovation',
      description: 'We continuously innovate to provide cutting-edge solutions that transform healthcare administration.'
    },
    {
      icon: '🤝',
      title: 'Trust',
      description: 'Building trust through transparency, reliability, and consistent delivery of our promises.'
    },
    {
      icon: '⚡',
      title: 'Efficiency',
      description: 'Streamlining processes to save time and reduce costs for all stakeholders in healthcare.'
    },
    {
      icon: '💚',
      title: 'Care',
      description: 'Putting patient care at the center of everything we do, improving access and outcomes.'
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

<section bind:this={sectionRef} class="about-page">
  <!-- Hero Section -->
  <div class="about-hero section">
    <div class="container">
      <div class="hero-content" class:animate={isVisible}>
        <h1 class="hero-title">About SimpleTPA</h1>
        <p class="hero-description">
          We're revolutionizing healthcare administration in the Philippines by connecting 
          employers, healthcare providers, and employees through innovative digital solutions.
        </p>
      </div>
    </div>
  </div>

  <!-- Mission & Vision -->
  <div class="mission-vision section">
    <div class="container">
      <div class="mission-vision-grid">
        <div class="mission-card">
          <div class="card-icon">🎯</div>
          <h2 class="card-title">Our Mission</h2>
          <p class="card-description">
            To simplify healthcare administration and make quality healthcare more accessible 
            and affordable for all Filipinos through innovative technology solutions.
          </p>
        </div>
        <div class="vision-card">
          <div class="card-icon">🔮</div>
          <h2 class="card-title">Our Vision</h2>
          <p class="card-description">
            To become the leading healthcare administration platform in Southeast Asia, 
            transforming how healthcare benefits are managed and delivered.
          </p>
        </div>
      </div>
    </div>
  </div>

  <!-- Company Story -->
  <div class="company-story section">
    <div class="container">
      <div class="story-content">
        <h2 class="section-title">Our Story</h2>
        <div class="story-text">
          <p>
            SimpleTPA was born out of a simple observation: healthcare administration in the Philippines 
            was fragmented, inefficient, and costly for everyone involved. Employers struggled with 
            complex benefit management, healthcare providers faced delayed reimbursements, and employees 
            found it difficult to access their benefits.
          </p>
          <p>
            Our founders, with their 118+ years of combined experience in building new markets for 
            life & health insurers like AIG, ING, HSBC & Pacific Cross, saw an opportunity to create 
            a unified platform that would address these challenges. SimpleTPA was founded as an 
            Administrative Services Only (ASO) company to streamline healthcare administration.
          </p>
          <p>
            Today, we're proud to work with leading healthcare providers across the Philippines, 
            helping companies save 30% or more on their healthcare administration costs while 
            providing same-day reimbursements and instant coverage approvals.
          </p>
        </div>
      </div>
    </div>
  </div>

  <!-- Timeline -->
  <div class="timeline-section section">
    <div class="container">
      <h2 class="section-title text-center">Our Journey</h2>
      <div class="timeline">
        {#each milestones as milestone, index}
          <div class="milestone" style="--delay: {index * 0.2}s">
            <div class="milestone-year">{milestone.year}</div>
            <div class="milestone-content">
              <h3 class="milestone-title">{milestone.title}</h3>
              <p class="milestone-description">{milestone.description}</p>
            </div>
          </div>
        {/each}
      </div>
    </div>
  </div>

  <!-- Values -->
  <div class="values-section section">
    <div class="container">
      <h2 class="section-title text-center">Our Values</h2>
      <div class="values-grid">
        {#each values as value, index}
          <div class="value-card" style="--delay: {index * 0.1}s">
            <div class="value-icon">{value.icon}</div>
            <h3 class="value-title">{value.title}</h3>
            <p class="value-description">{value.description}</p>
          </div>
        {/each}
      </div>
    </div>
  </div>

  <!-- Team -->
  <div class="team-section section">
    <div class="container">
      <h2 class="section-title text-center">Leadership Team</h2>
      <div class="team-grid">
        {#each team as member, index}
          <div class="team-card" style="--delay: {index * 0.1}s">
            <div class="member-avatar">
              <span class="avatar-initial">{member.initial}</span>
            </div>
            <div class="member-info">
              <h3 class="member-name">{member.name}</h3>
              <div class="member-role">{member.role}</div>
              <p class="member-description">{member.description}</p>
            </div>
          </div>
        {/each}
      </div>
    </div>
  </div>
</section>

<style>
  .about-page {
    padding-top: 0;
  }

  /* Hero Section */
  .about-hero {
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

  /* Mission & Vision */
  .mission-vision {
    background-color: var(--color-bg-primary);
  }

  .mission-vision-grid {
    display: grid;
    gap: var(--space-8);
    grid-template-columns: 1fr;
  }

  @media (min-width: 1024px) {
    .mission-vision-grid {
      grid-template-columns: repeat(2, 1fr);
    }
  }

  .mission-card,
  .vision-card {
    text-align: center;
    padding: var(--space-8);
    background: linear-gradient(135deg, var(--color-bg-secondary) 0%, var(--color-bg-tertiary) 100%);
    border: 1px solid var(--color-border);
    border-radius: var(--radius-lg);
    transition: all 0.3s ease-out;
  }

  .mission-card:hover,
  .vision-card:hover {
    transform: translateY(-4px);
    box-shadow: var(--shadow-lg);
  }

  .card-icon {
    font-size: 48px;
    margin-bottom: var(--space-4);
  }

  .card-title {
    font-size: var(--text-2xl);
    font-weight: var(--font-weight-bold);
    color: var(--color-text-primary);
    margin-bottom: var(--space-4);
  }

  .card-description {
    font-size: var(--text-base);
    color: var(--color-text-secondary);
    line-height: var(--leading-relaxed);
  }

  /* Company Story */
  .company-story {
    background: linear-gradient(180deg, var(--color-bg-primary) 0%, var(--color-bg-secondary) 100%);
  }

  .story-content {
    max-width: 800px;
    margin: 0 auto;
    text-align: center;
  }

  .section-title {
    font-size: var(--text-3xl);
    font-weight: var(--font-weight-bold);
    color: var(--color-text-primary);
    margin-bottom: var(--space-8);
  }

  @media (min-width: 768px) {
    .section-title {
      font-size: var(--text-4xl);
    }
  }

  .story-text {
    display: flex;
    flex-direction: column;
    gap: var(--space-6);
  }

  .story-text p {
    font-size: var(--text-lg);
    color: var(--color-text-secondary);
    line-height: var(--leading-relaxed);
    text-align: left;
  }

  /* Timeline */
  .timeline-section {
    background-color: var(--color-bg-secondary);
  }

  .timeline {
    max-width: 800px;
    margin: 0 auto;
    position: relative;
  }

  .timeline::before {
    content: '';
    position: absolute;
    left: 20px;
    top: 0;
    bottom: 0;
    width: 2px;
    background: linear-gradient(180deg, var(--color-accent) 0%, var(--color-success) 100%);
  }

  @media (min-width: 768px) {
    .timeline::before {
      left: 50%;
      transform: translateX(-50%);
    }
  }

  .milestone {
    position: relative;
    padding: var(--space-6) 0 var(--space-6) 60px;
    opacity: 0;
    transform: translateX(-20px);
    animation: slideInLeft 0.6s ease-out calc(0.2s + var(--delay)) forwards;
  }

  @media (min-width: 768px) {
    .milestone {
      width: 50%;
      padding: var(--space-6) var(--space-8);
      transform: translateX(20px);
    }

    .milestone:nth-child(even) {
      margin-left: 50%;
      transform: translateX(-20px);
    }

    .milestone:nth-child(even)::before {
      right: 100%;
      left: auto;
      margin-right: -6px;
    }
  }

  .milestone::before {
    content: '';
    position: absolute;
    left: 14px;
    top: var(--space-6);
    width: 12px;
    height: 12px;
    border-radius: 50%;
    background: var(--color-accent);
    border: 2px solid var(--color-bg-secondary);
  }

  @media (min-width: 768px) {
    .milestone::before {
      left: -6px;
    }
  }

  @keyframes slideInLeft {
    to {
      opacity: 1;
      transform: translateX(0);
    }
  }

  .milestone-year {
    font-size: var(--text-sm);
    font-weight: var(--font-weight-bold);
    color: var(--color-accent);
    text-transform: uppercase;
    letter-spacing: 0.1em;
    margin-bottom: var(--space-2);
  }

  .milestone-title {
    font-size: var(--text-xl);
    font-weight: var(--font-weight-bold);
    color: var(--color-text-primary);
    margin-bottom: var(--space-3);
  }

  .milestone-description {
    font-size: var(--text-base);
    color: var(--color-text-secondary);
    line-height: var(--leading-relaxed);
  }

  /* Values */
  .values-section {
    background-color: var(--color-bg-primary);
  }

  .values-grid {
    display: grid;
    gap: var(--space-8);
    grid-template-columns: 1fr;
  }

  @media (min-width: 768px) {
    .values-grid {
      grid-template-columns: repeat(2, 1fr);
    }
  }

  @media (min-width: 1024px) {
    .values-grid {
      grid-template-columns: repeat(4, 1fr);
    }
  }

  .value-card {
    text-align: center;
    padding: var(--space-6);
    background: linear-gradient(135deg, var(--color-bg-secondary) 0%, var(--color-bg-tertiary) 100%);
    border: 1px solid var(--color-border);
    border-radius: var(--radius-lg);
    opacity: 0;
    transform: translateY(20px);
    animation: fadeInUp 0.5s ease-out calc(0.3s + var(--delay)) forwards;
    transition: all 0.3s ease-out;
  }

  .value-card:hover {
    transform: translateY(-4px);
    box-shadow: var(--shadow);
  }

  @keyframes fadeInUp {
    to {
      opacity: 1;
      transform: translateY(0);
    }
  }

  .value-icon {
    font-size: 40px;
    margin-bottom: var(--space-4);
  }

  .value-title {
    font-size: var(--text-xl);
    font-weight: var(--font-weight-bold);
    color: var(--color-text-primary);
    margin-bottom: var(--space-3);
  }

  .value-description {
    font-size: var(--text-sm);
    color: var(--color-text-secondary);
    line-height: var(--leading-relaxed);
  }

  /* Team */
  .team-section {
    background: linear-gradient(180deg, var(--color-bg-primary) 0%, var(--color-bg-secondary) 100%);
  }

  .team-grid {
    display: grid;
    gap: var(--space-8);
    grid-template-columns: 1fr;
  }

  @media (min-width: 768px) {
    .team-grid {
      grid-template-columns: repeat(2, 1fr);
    }
  }

  .team-card {
    display: flex;
    flex-direction: column;
    align-items: center;
    text-align: center;
    padding: var(--space-8);
    background: linear-gradient(135deg, var(--color-bg-secondary) 0%, var(--color-bg-tertiary) 100%);
    border: 1px solid var(--color-border);
    border-radius: var(--radius-lg);
    opacity: 0;
    transform: translateY(20px);
    animation: fadeInUp 0.6s ease-out calc(0.4s + var(--delay)) forwards;
    transition: all 0.3s ease-out;
  }

  .team-card:hover {
    transform: translateY(-4px);
    box-shadow: var(--shadow-lg);
  }

  .member-avatar {
    width: 80px;
    height: 80px;
    border-radius: 50%;
    background: linear-gradient(135deg, var(--color-accent) 0%, var(--color-accent-hover) 100%);
    display: flex;
    align-items: center;
    justify-content: center;
    margin-bottom: var(--space-6);
  }

  .avatar-initial {
    font-size: var(--text-2xl);
    font-weight: var(--font-weight-bold);
    color: white;
  }

  .member-name {
    font-size: var(--text-xl);
    font-weight: var(--font-weight-bold);
    color: var(--color-text-primary);
    margin-bottom: var(--space-2);
  }

  .member-role {
    font-size: var(--text-base);
    font-weight: var(--font-weight-medium);
    color: var(--color-accent);
    margin-bottom: var(--space-4);
  }

  .member-description {
    font-size: var(--text-sm);
    color: var(--color-text-secondary);
    line-height: var(--leading-relaxed);
  }
</style>