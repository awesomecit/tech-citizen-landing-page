---
name: "[SPRINT 1] Task 1.4.1: Test DNS e Hosting"
about: Verifica configurazione DNS e test di connettività
title: "[S1-T1.4.1] Test DNS e Hosting"
labels: ['sprint-1', 'dns', 'deployment', 'priority-critical']
---

## 📋 Task Description

Verificare che il dominio tech-citizen.me sia configurato correttamente e testare la connettività HTTPS.

## 🎯 Acceptance Criteria

- [ ] DNS risolve correttamente su più server DNS
- [ ] HTTPS funzionante senza errori certificato
- [ ] Script di test DNS automatizzato
- [ ] Connettività verificata da più provider
- [ ] Latenza accettabile (< 500ms)

## 🔗 Dependencies

- **Depends on**: Configurazione dominio esterna
- **Blocks**: Task 1.4.2 (Test Deploy), Task 4.1.1 (Production Deploy)

## 📝 Implementation Notes

```bash
#!/bin/bash
# test-dns.sh
DOMAIN="tech-citizen.me"

echo "🌐 Testing DNS for: $DOMAIN"
for dns in "8.8.8.8" "1.1.1.1" "208.67.222.222"; do
    echo -n "  $dns: "
    result=$(nslookup "$DOMAIN" "$dns" 2>/dev/null | grep -A1 "Name:" | tail -1 | awk '{print $2}')
    [ -n "$result" ] && echo "✅ $result" || echo "❌ Not resolved"
done

echo "🔒 Testing HTTPS connectivity"
curl -I -s --max-time 10 "https://$DOMAIN" && echo "✅ Connected" || echo "❌ Failed"

echo "⚡ Testing latency"
ping -c 3 "$DOMAIN" | tail -1 | awk '{print $4}' | cut -d'/' -f2
```

## ✅ Definition of Done

- [ ] DNS risolve su tutti i server testati
- [ ] HTTPS risponde correttamente
- [ ] Script di test funzionante
- [ ] Latenza sotto 500ms
- [ ] Documentazione test procedure