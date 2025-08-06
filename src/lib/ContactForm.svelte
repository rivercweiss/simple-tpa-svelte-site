<script>
  let formData = $state({
    name: '',
    email: '',
    company: '',
    phone: '',
    subject: '',
    message: ''
  });

  let formStatus = $state('idle'); // 'idle', 'submitting', 'success', 'error'
  let errorMessage = $state('');

  async function handleSubmit(event) {
    event.preventDefault();
    formStatus = 'submitting';

    try {
      const response = await fetch('https://formsubmit.co/contactus@simpletpa.com', {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json',
        },
        body: JSON.stringify({
          name: formData.name,
          email: formData.email,
          company: formData.company,
          phone: formData.phone,
          subject: formData.subject,
          message: formData.message,
          _subject: `New inquiry from ${formData.name} - ${formData.subject}`,
          _captcha: 'false'
        })
      });

      if (response.ok) {
        formStatus = 'success';
        // Reset form
        formData = {
          name: '',
          email: '',
          company: '',
          phone: '',
          subject: '',
          message: ''
        };
      } else {
        throw new Error('Form submission failed');
      }
    } catch (error) {
      formStatus = 'error';
      errorMessage = 'Something went wrong. Please try again or contact us directly.';
    }
  }

  function resetForm() {
    formStatus = 'idle';
    errorMessage = '';
  }
</script>

<section class="contact-form-section section">
  <div class="container">
    <div class="form-container">
      <div class="form-header">
        <h2 class="form-title">Get Started with SimpleTPA</h2>
        <p class="form-description">
          Ready to streamline your healthcare administration and save costs? 
          Contact us today for a personalized consultation.
        </p>
      </div>

      <div class="form-wrapper">
        {#if formStatus === 'success'}
          <div class="success-message">
            <div class="success-icon">
              <svg width="48" height="48" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                <path d="M22 11.08V12a10 10 0 1 1-5.93-9.14"/>
                <path d="M9 11l3 3L22 4"/>
              </svg>
            </div>
            <h3 class="success-title">Thank you for your inquiry!</h3>
            <p class="success-text">
              We've received your message and will get back to you within 24 hours.
            </p>
            <button onclick={resetForm} class="btn-secondary">Send Another Message</button>
          </div>
        {:else}
          <form class="contact-form" onsubmit={handleSubmit}>
            <div class="form-grid">
              <div class="form-group">
                <label for="name" class="form-label">Full Name *</label>
                <input
                  type="text"
                  id="name"
                  name="name"
                  bind:value={formData.name}
                  class="form-input"
                  placeholder="Enter your full name"
                  required
                />
              </div>

              <div class="form-group">
                <label for="email" class="form-label">Email Address *</label>
                <input
                  type="email"
                  id="email"
                  name="email"
                  bind:value={formData.email}
                  class="form-input"
                  placeholder="Enter your email"
                  required
                />
              </div>

              <div class="form-group">
                <label for="company" class="form-label">Company</label>
                <input
                  type="text"
                  id="company"
                  name="company"
                  bind:value={formData.company}
                  class="form-input"
                  placeholder="Enter your company name"
                />
              </div>

              <div class="form-group">
                <label for="phone" class="form-label">Phone Number</label>
                <input
                  type="tel"
                  id="phone"
                  name="phone"
                  bind:value={formData.phone}
                  class="form-input"
                  placeholder="Enter your phone number"
                />
              </div>
            </div>

            <div class="form-group">
              <label for="subject" class="form-label">Subject *</label>
              <select
                id="subject"
                name="subject"
                bind:value={formData.subject}
                class="form-input form-select"
                required
              >
                <option value="">Select a subject</option>
                <option value="General Inquiry">General Inquiry</option>
                <option value="Employer/Company">Employer/Company Interest</option>
                <option value="Healthcare Provider">Healthcare Provider</option>
                <option value="Partnership">Partnership Opportunity</option>
                <option value="Support">Technical Support</option>
                <option value="Other">Other</option>
              </select>
            </div>

            <div class="form-group">
              <label for="message" class="form-label">Message *</label>
              <textarea
                id="message"
                name="message"
                bind:value={formData.message}
                class="form-input form-textarea"
                placeholder="Tell us about your healthcare administration needs..."
                rows="6"
                required
              ></textarea>
            </div>

            {#if formStatus === 'error'}
              <div class="error-message">
                <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <circle cx="12" cy="12" r="10"/>
                  <line x1="15" y1="9" x2="9" y2="15"/>
                  <line x1="9" y1="9" x2="15" y2="15"/>
                </svg>
                {errorMessage}
              </div>
            {/if}

            <div class="form-footer">
              <button
                type="submit"
                class="btn-primary form-submit"
                disabled={formStatus === 'submitting'}
              >
                {#if formStatus === 'submitting'}
                  <svg class="loading-spinner" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                    <path d="M21 12a9 9 0 11-6.219-8.56"/>
                  </svg>
                  Sending...
                {:else}
                  Send Message
                  <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                    <line x1="22" y1="2" x2="11" y2="13"/>
                    <polygon points="22,2 15,22 11,13 2,9"/>
                  </svg>
                {/if}
              </button>
            </div>
          </form>
        {/if}

        <!-- Contact Information -->
        <div class="contact-info">
          <h3 class="contact-info-title">Other Ways to Reach Us</h3>
          
          <div class="contact-methods">
            <div class="contact-method">
              <div class="method-icon">
                <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z"/>
                  <polyline points="22,6 12,13 2,6"/>
                </svg>
              </div>
              <div class="method-content">
                <div class="method-label">Email</div>
                <a href="mailto:contactus@simpletpa.com" class="method-value">contactus@simpletpa.com</a>
              </div>
            </div>

            <div class="contact-method">
              <div class="method-icon">
                <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <path d="M22 16.92v3a2 2 0 0 1-2.18 2 19.79 19.79 0 0 1-8.63-3.07 19.5 19.5 0 0 1-6-6 19.79 19.79 0 0 1-3.07-8.67A2 2 0 0 1 4.11 2h3a2 2 0 0 1 2 1.72 12.84 12.84 0 0 0 .7 2.81 2 2 0 0 1-.45 2.11L8.09 9.91a16 16 0 0 0 6 6l1.27-1.27a2 2 0 0 1 2.11-.45 12.84 12.84 0 0 0 2.81.7A2 2 0 0 1 22 16.92z"/>
                </svg>
              </div>
              <div class="method-content">
                <div class="method-label">Phone</div>
                <a href="tel:+639088928375" class="method-value">+63 (908) 892 8375</a>
              </div>
            </div>

            <div class="contact-method">
              <div class="method-icon">
                <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                  <path d="M21 10c0 7-9 13-9 13s-9-6-9-13a9 9 0 0 1 18 0z"/>
                  <circle cx="12" cy="10" r="3"/>
                </svg>
              </div>
              <div class="method-content">
                <div class="method-label">Office</div>
                <div class="method-value">7th Floor, Unit B, 8Rockwell<br>Hidalgo Drive, Rockwell Center<br>Makati, 1210, Philippines</div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>

<style>
  .contact-form-section {
    background: linear-gradient(180deg, var(--color-bg-primary) 0%, var(--color-bg-secondary) 100%);
  }

  .form-container {
    max-width: 800px;
    margin: 0 auto;
  }

  /* Form Header */
  .form-header {
    text-align: center;
    margin-bottom: var(--space-12);
  }

  .form-title {
    font-size: var(--text-3xl);
    font-weight: var(--font-weight-bold);
    color: var(--color-text-primary);
    margin-bottom: var(--space-4);
  }

  @media (min-width: 768px) {
    .form-title {
      font-size: var(--text-4xl);
    }
  }

  .form-description {
    font-size: var(--text-lg);
    color: var(--color-text-secondary);
    line-height: var(--leading-relaxed);
    max-width: 600px;
    margin: 0 auto;
  }

  /* Form Wrapper */
  .form-wrapper {
    background: linear-gradient(135deg, var(--color-bg-secondary) 0%, var(--color-bg-tertiary) 100%);
    border: 1px solid var(--color-border);
    border-radius: var(--radius-lg);
    padding: var(--space-8);
  }

  @media (min-width: 768px) {
    .form-wrapper {
      padding: var(--space-12);
    }
  }

  /* Contact Form */
  .contact-form {
    margin-bottom: var(--space-12);
  }

  .form-grid {
    display: grid;
    gap: var(--space-6);
    grid-template-columns: 1fr;
    margin-bottom: var(--space-6);
  }

  @media (min-width: 768px) {
    .form-grid {
      grid-template-columns: repeat(2, 1fr);
    }
  }

  .form-group {
    display: flex;
    flex-direction: column;
    gap: var(--space-2);
  }

  .form-label {
    font-size: var(--text-sm);
    font-weight: var(--font-weight-medium);
    color: var(--color-text-primary);
  }

  .form-input {
    padding: var(--space-4) var(--space-4);
    border: 1px solid var(--color-border);
    border-radius: var(--radius-md);
    background-color: var(--color-bg-primary);
    color: var(--color-text-primary);
    font-size: var(--text-base);
    font-family: var(--font-family);
    transition: all var(--transition-fast);
    min-height: 48px;
  }

  .form-input:focus {
    outline: none;
    border-color: var(--color-accent);
    box-shadow: 0 0 0 3px rgba(94, 106, 210, 0.1);
    transform: translateY(-1px);
  }

  .form-input::placeholder {
    color: var(--color-text-tertiary);
  }

  .form-textarea {
    resize: vertical;
    min-height: 120px;
  }

  .form-select {
    cursor: pointer;
  }

  /* Success Message */
  .success-message {
    text-align: center;
    padding: var(--space-12);
  }

  .success-icon {
    color: var(--color-success);
    margin-bottom: var(--space-4);
  }

  .success-title {
    font-size: var(--text-2xl);
    font-weight: var(--font-weight-bold);
    color: var(--color-text-primary);
    margin-bottom: var(--space-3);
  }

  .success-text {
    font-size: var(--text-base);
    color: var(--color-text-secondary);
    margin-bottom: var(--space-6);
  }

  /* Error Message */
  .error-message {
    display: flex;
    align-items: center;
    gap: var(--space-2);
    padding: var(--space-3) var(--space-4);
    background-color: rgba(239, 68, 68, 0.1);
    border: 1px solid rgba(239, 68, 68, 0.2);
    border-radius: var(--radius);
    color: #ef4444;
    font-size: var(--text-sm);
    margin-bottom: var(--space-6);
  }

  /* Form Footer */
  .form-footer {
    display: flex;
    justify-content: center;
    margin-top: var(--space-8);
  }

  .form-submit {
    min-width: 160px;
    position: relative;
  }

  .form-submit:disabled {
    opacity: 0.7;
    cursor: not-allowed;
    transform: none !important;
  }

  .loading-spinner {
    animation: spin 1s linear infinite;
  }

  @keyframes spin {
    from {
      transform: rotate(0deg);
    }
    to {
      transform: rotate(360deg);
    }
  }

  /* Contact Info */
  .contact-info {
    border-top: 1px solid var(--color-border);
    padding-top: var(--space-8);
  }

  .contact-info-title {
    font-size: var(--text-lg);
    font-weight: var(--font-weight-semibold);
    color: var(--color-text-primary);
    margin-bottom: var(--space-6);
    text-align: center;
  }

  .contact-methods {
    display: flex;
    flex-direction: column;
    gap: var(--space-4);
  }

  @media (min-width: 768px) {
    .contact-methods {
      flex-direction: row;
      justify-content: space-around;
    }
  }

  .contact-method {
    display: flex;
    align-items: center;
    gap: var(--space-3);
    text-align: center;
  }

  @media (min-width: 768px) {
    .contact-method {
      flex-direction: column;
      text-align: center;
    }
  }

  .method-icon {
    color: var(--color-accent);
    flex-shrink: 0;
  }

  .method-label {
    font-size: var(--text-sm);
    font-weight: var(--font-weight-medium);
    color: var(--color-text-tertiary);
    margin-bottom: var(--space-1);
  }

  .method-value {
    font-size: var(--text-sm);
    color: var(--color-text-secondary);
    text-decoration: none;
    transition: color var(--transition-fast);
  }

  .method-value:hover {
    color: var(--color-accent);
  }
</style>