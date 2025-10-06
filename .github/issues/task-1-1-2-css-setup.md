---
name: "[SPRINT 1] Task 1.1.2: Setup Framework CSS"
about: Integrazione Tailwind CSS e struttura CSS personalizzata
title: "[S1-T1.1.2] Setup Framework CSS"
labels: ['sprint-1', 'foundation', 'css', 'priority-high']
---

## 📋 Task Description

Integrare Tailwind CSS via CDN e creare la struttura CSS personalizzata per estendere il framework.

## 🎯 Acceptance Criteria

- [ ] Tailwind CSS integrato via CDN in `index.html`
- [ ] File `css/custom.css` creato per personalizzazioni
- [ ] CSS personalizzato caricato dopo Tailwind
- [ ] Verificata applicazione classi Tailwind di base
- [ ] Setup responsive breakpoints configurato

## 🔗 Dependencies

- **Depends on**: Task 1.1.1 (Struttura HTML)
- **Blocks**: Task 1.3.2 (Base Component), Task 2.1.1 (Hero Component)

## 📝 Implementation Notes

```html
<!-- In index.html head -->
<link href="https://cdn.tailwindcss.com" rel="stylesheet">
<link href="./css/custom.css" rel="stylesheet">
```

```css
/* css/custom.css */
/* Custom Tailwind extensions */
@layer utilities {
  .hero-gradient {
    background: linear-gradient(135deg, #1e40af 0%, #3b82f6 100%);
  }
}

/* Component-specific styles */
.cta-button {
  @apply bg-amber-500 hover:bg-amber-600 text-white font-bold py-3 px-6 rounded-lg transition-colors;
}
```

## ✅ Definition of Done

- [ ] Tailwind CSS caricato correttamente
- [ ] Custom CSS applicato senza conflitti
- [ ] Breakpoints responsive funzionanti
- [ ] Nessun errore console CSS
- [ ] Preparato per componenti LitElement