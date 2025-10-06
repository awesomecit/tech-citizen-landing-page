---
name: "[SPRINT 1] Task 1.3.3: Main App Component"
about: Creazione del componente principale dell'applicazione
title: "[S1-T1.3.3] Main App Component"
labels: ['sprint-1', 'litelement', 'app', 'priority-high']
---

## 📋 Task Description

Creare il componente principale `TechCitizenApp` che orchestrerà tutte le sezioni della landing page.

## 🎯 Acceptance Criteria

- [ ] Componente `TechCitizenApp` in `js/main.js`
- [ ] Bootstrap dell'applicazione nel DOM
- [ ] Struttura layout principale (header, main, footer)
- [ ] Integrazione i18n service al bootstrap
- [ ] Componente registrato e funzionante

## 🔗 Dependencies

- **Depends on**: Task 1.3.2 (BaseSection), Task 1.2.1 (i18n Service)
- **Blocks**: Task 2.1.1 (Hero Section)

## 📝 Implementation Notes

```javascript
// js/main.js
import { LitElement, html, css } from 'lit';
import { i18nService } from './i18n/i18n.js';
import './components/hero-section.js';

class TechCitizenApp extends LitElement {
  static styles = css`
    :host {
      display: block;
      min-height: 100vh;
    }
  `;

  async connectedCallback() {
    super.connectedCallback();
    await i18nService.loadTranslations();
    this.requestUpdate();
  }

  render() {
    return html`
      <header><!-- Navigation placeholder --></header>
      <main>
        <hero-section></hero-section>
      </main>
      <footer><!-- Footer placeholder --></footer>
    `;
  }
}

customElements.define('tech-citizen-app', TechCitizenApp);

// Bootstrap app
document.getElementById('app').innerHTML = '<tech-citizen-app></tech-citizen-app>';
```

## ✅ Definition of Done

- [ ] App component implementato
- [ ] i18n service caricato al bootstrap
- [ ] Layout principale strutturato
- [ ] App renderizzata correttamente
- [ ] Pronta per aggiunta sezioni
