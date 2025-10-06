---
name: "[SPRINT 1] Task 1.3.1: Setup LitElement Infrastructure"
about: Configurazione LitElement via CDN con ES6 modules
title: "[S1-T1.3.1] Setup LitElement Infrastructure"
labels: ['sprint-1', 'litelement', 'infrastructure', 'priority-high']
---

## 📋 Task Description

Configurare LitElement via Skypack CDN con importmap per ES6 modules e verificare il funzionamento base.

## 🎯 Acceptance Criteria

- [ ] Importmap configurato in `index.html`
- [ ] LitElement caricato da Skypack CDN
- [ ] ES6 modules funzionanti nel browser
- [ ] Test component di base creato e funzionante
- [ ] Console browser senza errori di caricamento

## 🔗 Dependencies

- **Depends on**: Task 1.1.1 (Struttura HTML), Task 1.1.3 (Struttura File)
- **Blocks**: Task 1.3.2 (Base Component), Task 1.3.3 (Main App)

## 📝 Implementation Notes

```html
<!-- In index.html head -->
<script type="importmap">
{
  "imports": {
    "lit": "https://cdn.skypack.dev/lit@2"
  }
}
</script>
```

```javascript
// Test component per verificare funzionamento
import { LitElement, html, css } from 'lit';

class TestComponent extends LitElement {
  static styles = css`
    :host {
      display: block;
      padding: 1rem;
      background: #f0f0f0;
    }
  `;

  render() {
    return html`
      <p>✅ LitElement funziona correttamente!</p>
    `;
  }
}

customElements.define('test-component', TestComponent);
```

## ✅ Definition of Done

- [ ] Importmap configurato correttamente
- [ ] LitElement caricato senza errori
- [ ] Test component renderizzato correttamente
- [ ] ES6 modules import/export funzionanti
- [ ] Browser compatibility verificata (Chrome, Firefox, Safari)