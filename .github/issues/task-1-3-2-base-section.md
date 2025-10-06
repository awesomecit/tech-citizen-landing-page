---
name: "[SPRINT 1] Task 1.3.2: Classe BaseSection"
about: Implementazione della classe base per tutti i componenti sezione
title: "[S1-T1.3.2] Classe BaseSection"
labels: ['sprint-1', 'litelement', 'architecture', 'priority-high']
---

## 📋 Task Description

Creare la classe astratta `BaseSection` che fornisce funzionalità comuni a tutti i componenti sezione (i18n, analytics, template method pattern).

## 🎯 Acceptance Criteria

- [ ] Classe `BaseSection` implementata in `js/components/base-section.js`
- [ ] Template method pattern implementato
- [ ] Integrazione i18n con funzione `t()`
- [ ] Metodo `trackEvent()` per analytics
- [ ] Stili CSS base comuni definiti

## 🔗 Dependencies

- **Depends on**: Task 1.3.1 (LitElement Setup), Task 1.2.1 (i18n Service)
- **Blocks**: Task 2.1.1 (Hero Section), Task 2.2.2 (Services Component)

## 📝 Implementation Notes

```javascript
// js/components/base-section.js
import { LitElement, html, css } from 'lit';
import { t } from '../i18n/i18n.js';

export class BaseSection extends LitElement {
  static styles = css`
    :host {
      display: block;
    }
    .section-container {
      @apply py-16;
    }
    .container {
      @apply mx-auto px-4 max-w-6xl;
    }
  `;
  
  // Template method pattern - override in child classes
  render() {
    return html`
      <section class="section-container">
        <div class="container">
          ${this.renderContent()}
        </div>
      </section>
    `;
  }
  
  // Abstract method - must be implemented by children
  renderContent() {
    return html`<p>Base section - override renderContent()</p>`;
  }
  
  // Common i18n integration
  t(key, params = {}) {
    return t(key, params);
  }
  
  // Analytics tracking point
  trackEvent(eventName, data = {}) {
    console.log('Track:', eventName, data);
    // Integration point for analytics service
    if (window.analytics && window.analytics.track) {
      window.analytics.track(eventName, data);
    }
  }
  
  // Lifecycle hook for analytics
  connectedCallback() {
    super.connectedCallback();
    this.trackEvent('section_view', { 
      section: this.constructor.name.toLowerCase() 
    });
  }
}
```

## ✅ Definition of Done

- [ ] BaseSection implementata e testata
- [ ] Template method pattern funzionante
- [ ] i18n integrazione verificata
- [ ] Analytics tracking hook presente
- [ ] Stili CSS base applicati correttamente