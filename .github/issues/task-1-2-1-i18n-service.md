---
name: "[SPRINT 1] Task 1.2.1: Sistema i18n Base"
about: Creazione del servizio di internazionalizzazione
title: "[S1-T1.2.1] Sistema i18n Base"
labels: ['sprint-1', 'i18n', 'service', 'priority-high']
---

## 📋 Task Description

Implementare il servizio di internazionalizzazione con supporto per chiavi dot-notation e interpolazione parametri.

## 🎯 Acceptance Criteria

- [ ] Classe `I18nService` implementata in `js/i18n/i18n.js`
- [ ] Metodo `t(key, params)` funzionante
- [ ] Supporto dot-notation per chiavi annidate
- [ ] Interpolazione parametri con `{{param}}`
- [ ] Fallback alla chiave se traduzione mancante

## 🔗 Dependencies

- **Depends on**: Task 1.1.3 (Struttura File)
- **Blocks**: Task 1.2.2 (Traduzioni Italiane), Task 1.3.2 (Base Component)

## 📝 Implementation Notes

```javascript
// js/i18n/i18n.js
class I18nService {
  constructor() {
    this.locale = 'it';
    this.translations = {};
  }
  
  async loadTranslations() {
    const response = await fetch(`./js/i18n/locales/${this.locale}.json`);
    this.translations = await response.json();
  }
  
  t(key, params = {}) {
    const keys = key.split('.');
    let value = this.translations;
    
    for (const k of keys) {
      value = value?.[k];
    }
    
    return value ? this.interpolate(value, params) : key;
  }
  
  interpolate(template, params) {
    return template.replace(/\{\{(\w+)\}\}/g, (match, key) => {
      return params[key] || match;
    });
  }
}

export const i18nService = new I18nService();
export const t = (key, params) => i18nService.t(key, params);
```

## ✅ Definition of Done

- [ ] Servizio i18n implementato e testato
- [ ] Funzione `t()` accessibile globalmente
- [ ] Dot-notation funzionante per chiavi annidate
- [ ] Interpolazione parametri testata
- [ ] Gestione errori per traduzioni mancanti