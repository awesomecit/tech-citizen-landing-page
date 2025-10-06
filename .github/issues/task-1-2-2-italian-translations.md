---
name: "[SPRINT 1] Task 1.2.2: File Traduzioni Italiane"
about: Creazione del file JSON con tutte le traduzioni italiane
title: "[S1-T1.2.2] File Traduzioni Italiane"
labels: ['sprint-1', 'i18n', 'content', 'priority-high']
---

## 📋 Task Description

Creare il file JSON con tutte le traduzioni italiane organizzate per sezioni con struttura dot-notation.

## 🎯 Acceptance Criteria

- [ ] File `js/i18n/locales/it.json` creato
- [ ] Traduzioni organizzate per sezioni (HERO, SERVICES, etc.)
- [ ] Struttura dot-notation implementata
- [ ] Tutti i testi della landing page tradotti
- [ ] JSON validato sintatticamente

## 🔗 Dependencies

- **Depends on**: Task 1.2.1 (Sistema i18n)
- **Blocks**: Task 2.1.1 (Hero Section), Task 2.2.1 (Services Data)

## 📝 Implementation Notes

```json
{
  "HERO": {
    "TITLE": "Trasformazione Agile Enterprise",
    "SUBTITLE": "con Intelligenza Emotiva",
    "DESCRIPTION": "Fractional CTO • Formazione • Agile",
    "CTA_BUTTON": "Richiedi Consulenza Strategica",
    "BENEFITS": {
      "EXPERIENCE": "15+ anni esperienza enterprise",
      "AGILE": "Metodologie Agile certificate",
      "LEADERSHIP": "Leadership emotivamente intelligente"
    }
  },
  "SERVICES": {
    "TITLE": "I Nostri Servizi",
    "SOFTWARE_DEV": {
      "TITLE": "Sviluppo Software",
      "DESCRIPTION": "Architetture moderne e scalabili"
    },
    "TRAINING": {
      "TITLE": "Formazione Enterprise",
      "DESCRIPTION": "Agile, Scrum, Leadership"
    },
    "CTO": {
      "TITLE": "Fractional CTO",
      "DESCRIPTION": "Strategia e leadership tecnica"
    }
  },
  "PROJECTS": {
    "TITLE": "Progetti & Case Study",
    "EMPTY_STATE": "Progetti in arrivo...",
    "LOADING": "Caricamento progetti..."
  },
  "ABOUT": {
    "TITLE": "Chi Sono",
    "DESCRIPTION": "Consulente senior con focus su trasformazione Agile e intelligenza emotiva in contesti enterprise.",
    "CERTIFICATIONS": {
      "SCRUM": "Certified Scrum Master",
      "EMOTIONAL": "Emotional Intelligence Coach",
      "CTO": "Fractional CTO Certified",
      "TRAINER": "Corporate Trainer"
    },
    "QUOTE": "La tecnologia è potente, ma le persone fanno la differenza."
  },
  "CONTACT": {
    "TITLE": "Contattami",
    "FORM": {
      "NAME": "Nome Completo",
      "COMPANY": "Azienda",
      "EMAIL": "Email",
      "ROLE": "Ruolo",
      "CHALLENGE": "Sfida principale",
      "SUBMIT": "Invia Richiesta"
    },
    "SUCCESS": "Messaggio inviato con successo!",
    "ERRORS": {
      "REQUIRED": "Campo obbligatorio",
      "EMAIL": "Email non valida"
    }
  }
}
```

## ✅ Definition of Done

- [ ] File JSON creato e validato
- [ ] Tutte le sezioni coperte
- [ ] Chiavi dot-notation consistenti
- [ ] Testi italiani corretti e professionali
- [ ] Integrazione con i18nService testata