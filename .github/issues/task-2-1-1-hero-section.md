---
name: "[SPRINT 2] Task 2.1.1: Hero Section Component"
about: Implementazione sezione hero con CTA e benefici
title: "[S2-T2.1.1] Hero Section Component"
labels: ['sprint-2', 'hero', 'component', 'priority-critical']
---

## 📋 Task Description

Implementare la sezione hero con titolo, sottotitolo, CTA button e grid dei benefici chiave. Prima sezione visibile per conversion.

## 🎯 Acceptance Criteria

- [ ] Componente `HeroSection` extends `BaseSection`
- [ ] Titolo, sottotitolo e descrizione da i18n
- [ ] CTA button con evento click e analytics
- [ ] Grid benefici responsiva (3 colonne desktop, 1 mobile)
- [ ] Gradient background e styling Tailwind

## 🔗 Dependencies

- **Depends on**: Task 1.3.2 (BaseSection), Task 1.2.2 (Traduzioni)
- **Blocks**: Task 2.1.2 (Hero Responsive), Task 2.5.1 (Contact Form)

## 📝 Implementation Notes

```javascript
// js/components/hero-section.js
import { BaseSection } from './base-section.js';
import { html, css } from 'lit';

export class HeroSection extends BaseSection {
  static styles = [
    super.styles,
    css`
      .hero-gradient {
        background: linear-gradient(135deg, #1e40af 0%, #3b82f6 100%);
      }
      .cta-button {
        @apply bg-amber-500 hover:bg-amber-600 text-white font-bold py-3 px-6 rounded-lg transition-colors;
      }
    `
  ];

  renderContent() {
    return html`
      <div class="hero-gradient text-white py-20">
        <div class="container mx-auto px-4 text-center">
          <h1 class="text-4xl md:text-6xl font-bold mb-4">
            ${this.t('HERO.TITLE')}
          </h1>
          <h2 class="text-xl md:text-2xl mb-6">
            ${this.t('HERO.SUBTITLE')}
          </h2>
          <p class="text-lg mb-8">
            ${this.t('HERO.DESCRIPTION')}
          </p>
          <button 
            class="cta-button"
            @click="${this.handleCTAClick}">
            ${this.t('HERO.CTA_BUTTON')}
          </button>
          
          <div class="mt-12 grid grid-cols-1 md:grid-cols-3 gap-6 text-sm">
            <div>✓ ${this.t('HERO.BENEFITS.EXPERIENCE')}</div>
            <div>✓ ${this.t('HERO.BENEFITS.AGILE')}</div>
            <div>✓ ${this.t('HERO.BENEFITS.LEADERSHIP')}</div>
          </div>
        </div>
      </div>
    `;
  }
  
  handleCTAClick() {
    this.trackEvent('hero_cta_click', { location: 'hero_section' });
    // Scroll to contact form when implemented
    const contactForm = document.querySelector('contact-form');
    if (contactForm) {
      contactForm.scrollIntoView({ behavior: 'smooth' });
    }
  }
}

customElements.define('hero-section', HeroSection);
```

## ✅ Definition of Done

- [ ] Hero section renderizzata correttamente
- [ ] Testi caricati da i18n
- [ ] CTA button funzionante con analytics
- [ ] Layout responsivo testato
- [ ] Gradient e styling applicati
