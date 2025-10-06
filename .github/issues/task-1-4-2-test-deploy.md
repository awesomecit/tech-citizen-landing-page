---
name: "[SPRINT 1] Task 1.4.2: Test Deploy Basico"
about: Deploy di test page per verificare hosting
title: "[S1-T1.4.2] Test Deploy Basico"
labels: ['sprint-1', 'deployment', 'test', 'priority-critical']
---

## 📋 Task Description

Creare e deployare una pagina di test semplice per verificare che l'hosting funzioni correttamente prima dello sviluppo completo.

## 🎯 Acceptance Criteria

- [ ] Pagina HTML di test creata
- [ ] Deploy effettuato su tech-citizen.me
- [ ] Pagina accessibile via HTTPS
- [ ] Meta tags SEO base presenti
- [ ] Messaggio "Coming Soon" professionale

## 🔗 Dependencies

- **Depends on**: Task 1.4.1 (DNS Test)
- **Blocks**: Task 4.1.1 (Production Deploy)

## 📝 Implementation Notes

```html
<!DOCTYPE html>
<html lang="it">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Tech Citizen - Coming Soon</title>
    <meta name="description" content="Consulenza Software Enterprise - Fractional CTO - Coming Soon">
    <style>
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            margin: 0;
            padding: 0;
            min-height: 100vh;
            background: linear-gradient(135deg, #1e40af 0%, #3b82f6 100%);
            display: flex;
            align-items: center;
            justify-content: center;
            color: white;
            text-align: center;
        }
        .container {
            max-width: 600px;
            padding: 2rem;
        }
        h1 {
            font-size: 3rem;
            margin-bottom: 1rem;
            font-weight: 700;
        }
        p {
            font-size: 1.2rem;
            margin-bottom: 2rem;
            opacity: 0.9;
        }
        .coming-soon {
            background: rgba(255,255,255,0.1);
            padding: 1rem 2rem;
            border-radius: 50px;
            backdrop-filter: blur(10px);
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Tech Citizen</h1>
        <p>Consulenza Software Enterprise<br>Fractional CTO • Agile Transformation</p>
        <div class="coming-soon">
            <strong>🚀 Coming Soon</strong>
        </div>
    </div>
</body>
</html>
```

## ✅ Definition of Done

- [ ] Pagina test creata e validata
- [ ] Deploy completato con successo
- [ ] Pagina accessibile da browser
- [ ] Meta tags presenti e corretti
- [ ] Design professionale e responsive