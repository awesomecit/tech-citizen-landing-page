---
name: "[SPRINT 2] Task 2.5.1: Contact Form Component"
about: Form di contatto con validazione e gestione stati
title: "[S2-T2.5.1] Contact Form Component"
labels: ['sprint-2', 'contact', 'form', 'priority-critical']
---

## 📋 Task Description

Implementare form di contatto completo con validazione client-side, gestione stati (loading, success, error) e integrazione analytics.

## 🎯 Acceptance Criteria

- [ ] Componente `ContactForm` extends `BaseSection`
- [ ] Campi: nome, azienda, email, ruolo, sfida
- [ ] Validazione client-side con messaggi errore
- [ ] Stati: default, submitting, success, error
- [ ] Analytics tracking per submit e errori

## 🔗 Dependencies

- **Depends on**: Task 1.3.2 (BaseSection), Task 1.2.2 (Traduzioni)
- **Blocks**: Nessuno (MVP ready)

## 📝 Implementation Notes

```javascript
// js/components/contact-form.js
import { BaseSection } from './base-section.js';
import { html, css } from 'lit';

export class ContactForm extends BaseSection {
  static properties = {
    formData: { type: Object },
    submitting: { type: Boolean },
    submitted: { type: Boolean },
    errors: { type: Object }
  };

  constructor() {
    super();
    this.formData = {
      name: '', company: '', email: '', role: '', challenge: ''
    };
    this.submitting = false;
    this.submitted = false;
    this.errors = {};
  }

  validateForm() {
    const errors = {};
    
    if (!this.formData.name.trim()) {
      errors.name = this.t('CONTACT.ERRORS.REQUIRED');
    }
    
    if (!this.formData.email.trim()) {
      errors.email = this.t('CONTACT.ERRORS.REQUIRED');
    } else if (!/\S+@\S+\.\S+/.test(this.formData.email)) {
      errors.email = this.t('CONTACT.ERRORS.EMAIL');
    }
    
    this.errors = errors;
    return Object.keys(errors).length === 0;
  }

  async handleSubmit(e) {
    e.preventDefault();
    
    if (!this.validateForm()) {
      this.trackEvent('form_validation_error', { errors: Object.keys(this.errors) });
      return;
    }

    this.submitting = true;
    
    try {
      // Simulate API call
      await new Promise(resolve => setTimeout(resolve, 1000));
      
      this.submitted = true;
      this.trackEvent('contact_form_submit', { 
        company: this.formData.company,
        role: this.formData.role 
      });
    } catch (error) {
      this.trackEvent('contact_form_error', { error: error.message });
    } finally {
      this.submitting = false;
    }
  }

  renderContent() {
    if (this.submitted) {
      return html`
        <div class="success-message">
          ${this.t('CONTACT.SUCCESS')}
        </div>
      `;
    }

    return html`
      <div class="max-w-2xl mx-auto">
        <h2 class="text-3xl font-bold text-center mb-8">
          ${this.t('CONTACT.TITLE')}
        </h2>
        
        <form @submit="${this.handleSubmit}">
          <!-- Form fields implementation -->
          <button 
            type="submit" 
            class="submit-button"
            ?disabled="${this.submitting}">
            ${this.submitting ? 'Invio...' : this.t('CONTACT.FORM.SUBMIT')}
          </button>
        </form>
      </div>
    `;
  }
}

customElements.define('contact-form', ContactForm);
```

## ✅ Definition of Done

- [ ] Form funzionante con tutti i campi
- [ ] Validazione client-side implementata
- [ ] Stati gestiti correttamente
- [ ] Analytics tracking completo
- [ ] Design responsivo applicato
