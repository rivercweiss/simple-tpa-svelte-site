<script>
  import { onMount } from 'svelte';

  let isVisible = $state(false);
  let sectionRef;

  const jobs = [
    {
      id: 1,
      title: 'Head of Claims Administration',
      department: 'Operations',
      location: 'Manila',
      type: 'Full-time',
      experience: 'Minimum 8 years',
      reportsTo: 'President',
      description: 'Head of Claims and Customer Service for SIMPLeTPA. Subject matter expert for digital claims adjudication and management platform. Founding team member with opportunity to influence company, market and platform development.',
      responsibilities: [
        'Support design, implementation and continuous management of rapid claims management system',
        'Work with insurance and healthcare partners on claims processing coordination',
        'Direct and manage team of claims adjudicators and customer service specialists',
        'Monitor and audit claim trends for fraud or overutilization',
        'Address key decision making with customers and medical providers',
        'Draft and maintain risk management guidelines and policies'
      ],
      qualifications: [
        '8+ years of relevant experience in medical claims processing',
        'Demonstrated experience working with medical providers to resolve difficult claim cases',
        'History of innovative, creative and driven work',
        'Prefer graduate of medical, nursing or related medical certification programs',
        'Excellent written and verbal communication skills',
        'Knowledgeable on digital enterprise workspace productivity tools'
      ]
    },
    {
      id: 2,
      title: 'Svelte F/E Developer',
      department: 'Technology Team',
      location: 'Remote Work',
      type: 'Full-time',
      experience: 'Minimum 1 year with Svelte',
      reportsTo: 'Head of Technology',
      description: 'Looking for experienced front-end developer with strong preference for Svelte and React programming. Operate as the lead developer for all front-end development work.',
      responsibilities: [
        'Support design, implementation and continuous development of rapid claims management platform',
        'Work with team to rapidly implement new technologies on evolving platform',
        'Monitor and audit new technology trends for API and advanced systems integration',
        'Work as key team member for building customer-centric solutions',
        'Draft and maintain appropriate documentation of work'
      ],
      qualifications: [
        '5+ years of relevant experience in front-end programming',
        'Demonstrated experience working in agile, inter-dependent team based organization',
        'History of innovative, creative and driven work',
        'Prefer graduate with IT degree',
        'Clear written and verbal communication skills',
        'Knowledgeable on digital enterprise workspace productivity tools'
      ]
    },
    {
      id: 3,
      title: 'Medical Director',
      department: 'Operations',
      location: 'Manila',
      type: 'Full-time / Contract',
      experience: 'Minimum 3 years',
      reportsTo: 'President',
      description: 'Provide clear communication balancing medical outcomes with fiduciary responsibility. Review overall managed care standards for claims administration and monitor claims data for optimal medical outcomes.',
      responsibilities: [
        'Support design and implementation of rapid claims management system',
        'Work with insurance and healthcare partners on claims processing',
        'Work as teammate with Sales and Network Provider teams',
        'Set Standard Operating Procedures for claims management',
        'Monitor and audit claim trends for fraud or overutilization',
        'Address key decision making for special medical conditions'
      ],
      qualifications: [
        'Board certified physician eligible to receive and review medical records',
        'Demonstrated experience working with medical providers to resolve difficult claim cases',
        'History of innovative, creative and driven work',
        'Excellent written and verbal communication skills',
        'Knowledgeable on digital enterprise workspace productivity tools'
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

<section bind:this={sectionRef} class="careers-page">
  <!-- Hero Section -->
  <div class="hero-section section">
    <div class="container">
      <div class="hero-content" class:animate={isVisible}>
        <h1 class="hero-title">Join Our Team</h1>
        <p class="hero-description">
          Join our high-performance and fast moving team dedicated to improving healthcare administration. 
          As an early stage start-up, we are looking for people who are ambitious and imaginative in 
          exploring ways to make healthcare more efficient and efficacious for all our stakeholders: 
          Patients, Employers and Healthcare Providers.
        </p>
      </div>
    </div>
  </div>

  <!-- Job Listings -->
  <div class="jobs-section section">
    <div class="container">
      <h2 class="section-title">Current Openings</h2>
      
      <div class="jobs-grid">
        {#each jobs as job, index}
          <div class="job-card" style="--delay: {index * 0.1}s">
            <div class="job-header">
              <div class="job-title-section">
                <h3 class="job-title">{job.title}</h3>
                <div class="job-meta">
                  <span class="job-department">{job.department}</span>
                  <span class="job-separator">•</span>
                  <span class="job-location">{job.location}</span>
                  <span class="job-separator">•</span>
                  <span class="job-type">{job.type}</span>
                </div>
              </div>
            </div>

            <div class="job-content">
              <p class="job-description">{job.description}</p>

              <div class="job-details">
                <div class="job-detail">
                  <strong>Experience Required:</strong> {job.experience}
                </div>
                <div class="job-detail">
                  <strong>Reports to:</strong> {job.reportsTo}
                </div>
              </div>

              <div class="job-section">
                <h4 class="section-subtitle">Key Responsibilities</h4>
                <ul class="job-list">
                  {#each job.responsibilities as responsibility}
                    <li>{responsibility}</li>
                  {/each}
                </ul>
              </div>

              <div class="job-section">
                <h4 class="section-subtitle">Qualifications</h4>
                <ul class="job-list">
                  {#each job.qualifications as qualification}
                    <li>{qualification}</li>
                  {/each}
                </ul>
              </div>

              <div class="job-footer">
                <a href="/contact" class="apply-btn">
                  Apply Now
                  <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                    <path d="M7 17L17 7" />
                    <path d="M7 7h10v10" />
                  </svg>
                </a>
              </div>
            </div>
          </div>
        {/each}
      </div>
    </div>
  </div>

  <!-- Contact CTA -->
  <div class="cta-section section">
    <div class="container">
      <div class="cta-content">
        <h2 class="cta-title">Don't See Your Role?</h2>
        <p class="cta-description">
          We're always looking for talented individuals to join our team. 
          Send us your resume and let us know how you can contribute to transforming healthcare administration.
        </p>
        <a href="/contact" class="btn-primary">Contact Us</a>
      </div>
    </div>
  </div>
</section>

<style>
  .careers-page {
    padding-top: 0;
  }

  /* Hero Section */
  .hero-section {
    background: linear-gradient(135deg, var(--color-bg-primary) 0%, var(--color-bg-secondary) 100%);
    padding-top: var(--space-32);
  }

  .hero-content {
    text-align: center;
    max-width: 900px;
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

  /* Jobs Section */
  .jobs-section {
    background-color: var(--color-bg-primary);
  }

  .section-title {
    text-align: center;
    font-size: var(--text-3xl);
    font-weight: var(--font-weight-bold);
    color: var(--color-text-primary);
    margin-bottom: var(--space-12);
  }

  .jobs-grid {
    display: flex;
    flex-direction: column;
    gap: var(--space-8);
    max-width: 900px;
    margin: 0 auto;
  }

  .job-card {
    background: linear-gradient(135deg, var(--color-bg-secondary) 0%, var(--color-bg-tertiary) 100%);
    border: 1px solid var(--color-border);
    border-radius: var(--radius-lg);
    overflow: hidden;
    opacity: 0;
    transform: translateY(20px);
    animation: fadeInUp 0.6s ease-out calc(0.2s + var(--delay)) forwards;
    transition: all 0.3s ease-out;
  }

  .job-card:hover {
    transform: translateY(-4px);
    box-shadow: var(--shadow-lg);
  }

  @keyframes fadeInUp {
    to {
      opacity: 1;
      transform: translateY(0);
    }
  }

  .job-header {
    padding: var(--space-6);
    border-bottom: 1px solid var(--color-border);
    background: var(--color-bg-primary);
  }

  .job-title {
    font-size: var(--text-xl);
    font-weight: var(--font-weight-bold);
    color: var(--color-text-primary);
    margin-bottom: var(--space-2);
  }

  .job-meta {
    display: flex;
    align-items: center;
    gap: var(--space-2);
    flex-wrap: wrap;
  }

  .job-department,
  .job-location,
  .job-type {
    font-size: var(--text-sm);
    color: var(--color-text-secondary);
    font-weight: var(--font-weight-medium);
  }

  .job-separator {
    color: var(--color-text-tertiary);
    font-size: var(--text-sm);
  }

  .job-content {
    padding: var(--space-6);
  }

  .job-description {
    font-size: var(--text-base);
    color: var(--color-text-secondary);
    line-height: var(--leading-relaxed);
    margin-bottom: var(--space-6);
  }

  .job-details {
    display: flex;
    flex-direction: column;
    gap: var(--space-2);
    margin-bottom: var(--space-6);
    padding: var(--space-4);
    background: var(--color-bg-primary);
    border-radius: var(--radius);
    border: 1px solid var(--color-border);
  }

  .job-detail {
    font-size: var(--text-sm);
    color: var(--color-text-secondary);
  }

  .job-detail strong {
    color: var(--color-text-primary);
    font-weight: var(--font-weight-semibold);
  }

  .job-section {
    margin-bottom: var(--space-6);
  }

  .section-subtitle {
    font-size: var(--text-lg);
    font-weight: var(--font-weight-semibold);
    color: var(--color-text-primary);
    margin-bottom: var(--space-3);
  }

  .job-list {
    list-style: none;
    display: flex;
    flex-direction: column;
    gap: var(--space-2);
  }

  .job-list li {
    position: relative;
    padding-left: var(--space-6);
    font-size: var(--text-sm);
    color: var(--color-text-secondary);
    line-height: var(--leading-relaxed);
  }

  .job-list li::before {
    content: '•';
    position: absolute;
    left: 0;
    color: var(--color-accent);
    font-weight: var(--font-weight-bold);
  }

  .job-footer {
    margin-top: var(--space-8);
    padding-top: var(--space-6);
    border-top: 1px solid var(--color-border);
  }

  .apply-btn {
    display: inline-flex;
    align-items: center;
    gap: var(--space-2);
    padding: var(--space-3) var(--space-6);
    background: linear-gradient(135deg, var(--color-accent) 0%, var(--color-accent-hover) 100%);
    color: white;
    text-decoration: none;
    border-radius: var(--radius);
    font-size: var(--text-base);
    font-weight: var(--font-weight-medium);
    transition: all var(--transition-fast);
  }

  .apply-btn:hover {
    transform: translateY(-1px);
    box-shadow: var(--shadow);
    color: white;
  }

  /* CTA Section */
  .cta-section {
    background: var(--color-bg-secondary);
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
    line-height: var(--leading-relaxed);
    margin-bottom: var(--space-8);
  }
</style>