# 🏢 Guida Completa: Tech Citizen - Conformità Legale e Setup Tecnico

## 📋 Indice
1. [Registrazione Marchio "Tech Citizen"](#1-registrazione-marchio-tech-citizen)
2. [Conformità UE e Domini .me](#2-conformità-ue-e-domini-me)
3. [Email Personalizzata con Google Workspace](#3-email-personalizzata-con-google-workspace)

---

## 1. 📝 Registrazione Marchio "Tech Citizen"

### 🎯 Opzioni di Registrazione

#### **A. Marchio Europeo (MUE) - CONSIGLIATO**
**Copertura**: Tutti i 27 paesi UE + Islanda, Liechtenstein, Norvegia  
**Costo**: €850 (online) per 1 classe + €50 per la 2ª + €150 per classi aggiuntive  
**Durata**: 10 anni, rinnovabile indefinitamente  
**Autorità**: EUIPO (Ufficio dell'Unione Europea per la Proprietà Intellettuale)

#### **B. Marchio Nazionale Italiano**
**Copertura**: Solo Italia  
**Costo**: Circa €300-400 per una classe  
**Autorità**: UIBM (Ufficio Italiano Brevetti e Marchi)

### 🚀 Procedura Marchio UE (Raccomandato)

#### **Step 1: Ricerca di Anteriorità**
```bash
# Strumenti gratuiti EUIPO
1. TMview (https://www.tmdn.org/tmview/)
   - Cerca "Tech Citizen" 
   - Cerca "TechCitizen"
   - Cerca marchi simili in classe 42 (servizi informatici)

2. eSearch plus EUIPO
   - Ricerca avanzata per conflitti
```

#### **Step 2: Identificare Classi di Nizza**
**Classe 42**: Servizi scientifici e tecnologici
- Consulenza in materia di software
- Sviluppo di software
- Servizi di fractional CTO
- Formazione tecnica

**Classe 41**: Educazione e formazione (opzionale)
- Corsi di formazione per aziende
- Sviluppo di competenze IT

#### **Step 3: Deposito Online**
**Sito**: https://euipo.europa.eu/ohimportal/it/

**Documenti necessari**:
- Rappresentazione del marchio (logo + denominazione)
- Elenco dettagliato prodotti/servizi
- Dati del richiedente (azienda o persona fisica)

**Tempi**: 4-6 mesi se nessuna opposizione

#### **Step 4: Incentivi Disponibili**
**Marchi+ 2024 (Italia)**:
- Rimborso 75% delle spese per PMI
- Budget: €2 milioni per il 2024
- Include: tasse deposito + consulenza specialistica

### 💡 Suggerimenti Strategici

#### **Varianti da Considerare**
```
- "Tech Citizen" (denominativo)
- Logo + denominazione (figurativo)
- "TechCitizen" (una parola)
- "@tech-citizen" (con simbolo)
```

#### **Protezione Aggiuntiva**
- **Domini correlati**: .it, .eu, .com
- **Social media**: LinkedIn, Twitter, Instagram
- **Marchio internazionale**: Sistema di Madrid (se espansione extra-UE)

---

## 2. ⚖️ Conformità UE e Domini .me

### 🌐 Status Domini .me (Montenegro)

#### **Requisiti Tecnici**
✅ **Nessuna restrizione**: Chiunque può registrare domini .me  
✅ **Lunghezza**: 3-63 caratteri  
✅ **Supporto IDN**: Caratteri internazionali supportati  
✅ **Privacy**: WHOIS privacy disponibile  

#### **Status Montenegro vs UE**
🔶 **Montenegro**: Paese candidato UE (non ancora membro)  
🔶 **GDPR**: Montenegro ha leggi simili al GDPR (applicazione parziale)  
🔶 **Trasferimenti dati**: Montenegro non ha decisione di adeguatezza UE  

### 📜 Requisiti Legali Obbligatori per Landing Page

#### **A. GDPR Compliance (Obbligatorio)**

##### **1. Privacy Policy Completa**
```markdown
## Privacy Policy - Tech Citizen

### Titolare del Trattamento
Tech Citizen di [Nome Cognome]
Sede: [Indirizzo completo]
Email: privacy@tech-citizen.me
P.IVA: [Partita IVA]

### Dati Raccolti
- **Modulo contatti**: Nome, email, azienda, ruolo, messaggio
- **Analytics**: Dati anonimizzati di navigazione
- **Cookie tecnici**: Necessari per il funzionamento

### Base Giuridica
- Art. 6(1)(a) GDPR: Consenso per marketing
- Art. 6(1)(b) GDPR: Esecuzione contratto per servizi
- Art. 6(1)(f) GDPR: Interesse legittimo per analytics

### Diritti dell'Interessato
- Accesso, rettifica, cancellazione
- Portabilità dei dati
- Opposizione al trattamento
- Reclamo al Garante Privacy

### Conservazione
- Dati contatto: 2 anni
- Analytics: 26 mesi (Google)
- Cookie: vedi Cookie Policy

### Trasferimenti Extra-UE
- Google Analytics: USA (DPF adequacy decision)
- Server hosting: [specificare paese]

Data ultimo aggiornamento: [data]
```

##### **2. Cookie Policy Obbligatoria**
```markdown
## Cookie Policy - Tech Citizen

### Cosa sono i Cookie
I cookie sono piccoli file di testo memorizzati nel browser.

### Cookie Utilizzati

#### Cookie Tecnici (Nessun Consenso Richiesto)
- **Sessione**: Mantiene la sessione utente
- **Sicurezza**: Protezione CSRF
- **Preferenze**: Lingua, tema scuro/chiaro

#### Cookie Analitici (Consenso Richiesto)
- **Google Analytics**: 
  - Finalità: Statistiche anonime di utilizzo
  - Durata: 26 mesi
  - Trasferimento: USA (adequacy decision)
  
#### Come Disabilitare
- Browser: Impostazioni > Privacy > Cookie
- Google Analytics: Opt-out addon
- Nostro banner: Gestisci preferenze

### Aggiornamenti
Questa policy può essere aggiornata. Data ultima modifica: [data]
```

##### **3. Cookie Banner Conforme**
**Requisiti obbligatori 2024**:
```javascript
// Caratteristiche banner conformi
const cookieBanner = {
  // ✅ Obbligatorio
  bloccoPreventivo: true, // Blocca cookie non essenziali prima del consenso
  consensoSpecifico: true, // Separato per categoria
  facilePriorità: true, // Rifiuto facile quanto accettazione
  linguaggioChiaro: true, // Italiano comprensibile
  
  // ✅ Configurazione corretta
  defaultState: "nonConsent", // Non pre-selezionato
  categories: {
    necessary: { required: true, blocked: false },
    analytics: { required: false, blocked: true },
    marketing: { required: false, blocked: true }
  },
  
  // ❌ VIETATO
  cookieWall: false, // Non bloccare contenuti senza consenso
  preCheckbox: false, // Non pre-selezionare
  darkPatterns: false // Non influenzare scelta utente
};
```

#### **B. Altri Requisiti Legali**

##### **4. Terms of Service**
```markdown
## Termini e Condizioni - Tech Citizen

### Servizi Offerti
- Consulenza software enterprise
- Formazione tecnica e agile
- Servizi di Fractional CTO

### Condizioni Generali
- Legge applicabile: Italiana
- Foro competente: [Città]
- Risoluzione controversie: Mediazione obbligatoria

### Limitazioni di Responsabilità
[Standard per servizi di consulenza]

### Modifiche
Modifiche notificate con 30 giorni preavviso.
```

##### **5. Informazioni Legali Obbligatorie**
```html
<!-- Footer legale obbligatorio -->
<footer>
  <div class="legal-info">
    <p>Tech Citizen di [Nome Cognome]</p>
    <p>P.IVA: [Partita IVA] | Cod. Fisc.: [Codice Fiscale]</p>
    <p>Sede: [Indirizzo completo con CAP e Città]</p>
    <p>Email: info@tech-citizen.me | PEC: [se obbligatoria]</p>
    
    <div class="legal-links">
      <a href="/privacy-policy">Privacy Policy</a>
      <a href="/cookie-policy">Cookie Policy</a>
      <a href="/terms">Termini e Condizioni</a>
    </div>
    
    <p>© 2024 Tech Citizen. Tutti i diritti riservati.</p>
  </div>
</footer>
```

##### **6. Accessibilità (Raccomandato)**
Per conformità alla Legge Stanca (L. 4/2004):
```html
<!-- Dichiarazione accessibilità -->
<a href="/dichiarazione-accessibilita">Dichiarazione di Accessibilità</a>

<!-- Standard WCAG 2.1 AA -->
- Contrasto colori: minimo 4.5:1
- Navigazione da tastiera
- Alt text per immagini
- Struttura semantica HTML
```

### 🛡️ Implementazione Tecnica Conformità

#### **A. Cookie Management Script**
```javascript
// Implementazione conforme italiana
class CookieManager {
  constructor() {
    this.consent = {
      necessary: true,
      analytics: false,
      marketing: false
    };
    this.init();
  }
  
  init() {
    // Blocca tutti i script non essenziali
    this.blockScripts();
    // Mostra banner se primo accesso
    if (!this.hasConsent()) {
      this.showBanner();
    }
  }
  
  blockScripts() {
    // Blocca Google Analytics finché non c'è consenso
    if (!this.consent.analytics) {
      window['ga-disable-UA-XXXXXX-X'] = true;
    }
  }
  
  grantConsent(categories) {
    this.consent = { ...this.consent, ...categories };
    localStorage.setItem('cookie-consent', JSON.stringify({
      consent: this.consent,
      timestamp: Date.now(),
      version: '1.0'
    }));
    
    // Attiva servizi consentiti
    this.enableServices();
  }
}
```

#### **B. Plugin WordPress Consigliati**
- **CookieYes**: Conforme GDPR/ePrivacy
- **Complianz**: Plugin italiano completo
- **Cookie Notice**: Gratuito, configurabile

---

## 3. 📧 Email Personalizzata con Google Workspace

### 🚀 Setup Google Workspace per tech-citizen.me

#### **Step 1: Registrazione Google Workspace**
**Costo**: €5.40/utente/mese (Business Starter)  
**Incluso**: 30GB storage, email personalizzata, Meet, Docs  
**Sito**: https://workspace.google.com/

#### **Step 2: Verifica Dominio**
Google fornirà un record TXT da aggiungere in Cloudflare:
```dns
Type: TXT
Name: tech-citizen.me
Content: google-site-verification=XXXXXXXXXXXXXXX
TTL: Auto
```

#### **Step 3: Configurazione MX Records in Cloudflare**

##### **A. Accedi a Cloudflare Dashboard**
1. Vai su dash.cloudflare.com
2. Seleziona `tech-citizen.me`
3. Vai su **DNS** nel menu laterale

##### **B. Rimuovi MX Records Esistenti**
Elimina eventuali record MX presenti

##### **C. Aggiungi i MX Records di Google**
**Nuovo formato 2024 (Singolo record)**:
```dns
Type: MX
Name: tech-citizen.me (o @)
Mail server: smtp.google.com
Priority: 10
TTL: Auto
Proxy status: DNS only (grigio)
```

**Se Google richiede il formato legacy**:
```dns
MX  @  1    aspmx.l.google.com
MX  @  5    alt1.aspmx.l.google.com  
MX  @  5    alt2.aspmx.l.google.com
MX  @  10   alt3.aspmx.l.google.com
MX  @  10   alt4.aspmx.l.google.com
```

#### **Step 4: Record SPF (Anti-Spam)**
```dns
Type: TXT
Name: tech-citizen.me
Content: v=spf1 include:_spf.google.com ~all
TTL: Auto
```

#### **Step 5: Record DKIM (Autenticazione)**
1. In Google Admin Console > Apps > Gmail > Authenticate email
2. Seleziona dominio e genera record
3. Aggiungi in Cloudflare:
```dns
Type: TXT
Name: google._domainkey
Content: [lungo stringa fornita da Google]
TTL: Auto
```

#### **Step 6: Record DMARC (Protezione)**
```dns
Type: TXT  
Name: _dmarc
Content: v=DMARC1; p=quarantine; rua=mailto:dmarc@tech-citizen.me
TTL: Auto
```

### 📧 Configurazione Utenti Email

#### **Indirizzi Consigliati**
```
info@tech-citizen.me        # Generale
consulting@tech-citizen.me  # Servizi consulenza  
training@tech-citizen.me    # Formazione
contact@tech-citizen.me     # Contatti landing
noreply@tech-citizen.me     # Sistema automatico
admin@tech-citizen.me       # Amministrazione
```

#### **Alias Email Gratuiti**
In Google Admin puoi creare alias senza costo aggiuntivo:
```
marco@tech-citizen.me → info@tech-citizen.me
cto@tech-citizen.me → consulting@tech-citizen.me
```

### 🔧 Configurazione DNS Completa Cloudflare

```dns
# Record A principale (Proxy abilitato)
A    tech-citizen.me    91.99.165.92    Proxied (arancione)

# Record WWW
CNAME www    tech-citizen.me    Proxied (arancione)

# MX Records per Google Workspace  
MX   @    10    smtp.google.com    DNS only (grigio)

# Record TXT per verifiche
TXT  @    google-site-verification=...    Auto
TXT  @    v=spf1 include:_spf.google.com ~all    Auto
TXT  google._domainkey    v=DKIM1; k=rsa; p=...    Auto
TXT  _dmarc    v=DMARC1; p=quarantine; rua=mailto:dmarc@tech-citizen.me    Auto
```

### ⏰ Tempi di Propagazione
- **Verifica dominio**: 15 minuti - 1 ora
- **MX records**: 1-24 ore  
- **SPF/DKIM**: 2-48 ore
- **Email funzionante**: 24-72 ore massimo

### 🧪 Test Configurazione
```bash
# Test MX records
nslookup -type=MX tech-citizen.me

# Test SPF
nslookup -type=TXT tech-citizen.me

# Test DKIM  
nslookup -type=TXT google._domainkey.tech-citizen.me

# Test invio email
echo "Test" | mail -s "Test" info@tech-citizen.me
```

---

## 📋 Checklist Finale

### ✅ Marchio
- [ ] Ricerca anteriorità completata
- [ ] Classi di Nizza identificate (42, eventualmente 41)
- [ ] Domanda MUE depositata online
- [ ] Richiesto incentivo Marchi+ 2024 (se PMI)

### ✅ Conformità Legale
- [ ] Privacy Policy completa pubblicata
- [ ] Cookie Policy conforme GDPR
- [ ] Cookie banner implementato (blocco preventivo)
- [ ] Terms of Service pubblicati
- [ ] Informazioni legali in footer
- [ ] Dichiarazione accessibilità (opzionale)

### ✅ Email Personalizzata
- [ ] Google Workspace registrato
- [ ] Dominio verificato (TXT record)
- [ ] MX records configurati in Cloudflare
- [ ] SPF record aggiunto
- [ ] DKIM configurato e attivato
- [ ] DMARC implementato
- [ ] Primo utente creato e testato
- [ ] Alias email configurati

### 📊 Costi Totali Stimati

```
Marchio Europeo:           €850
Google Workspace (anno):   €65 (1 utente)
Consulenza legale:         €500-1000 (opzionale)
Plugin compliance:        €0-50 (se WordPress)

TOTALE:                    €1.415-1.965
```

### 🚨 Note Importanti

1. **Montenegro e GDPR**: Anche se .me non è UE, se servi clienti UE devi essere conforme GDPR
2. **Residenza fiscale**: Se lavori dall'Italia, serve P.IVA italiana indipendentemente dal dominio
3. **Cookie Policy**: Obbligo italiano anche per siti .me se target italiano
4. **Email backup**: Configura backup automatici Google Vault
5. **Monitoraggio marchio**: Usa Google Alerts per "Tech Citizen" + varianti

---

**🎯 Prossimi Passi Immediati:**

1. **Settimana 1**: Deposito marchio + verifica disponibilità
2. **Settimana 2**: Setup Google Workspace + DNS
3. **Settimana 3**: Implementazione conformità GDPR
4. **Settimana 4**: Test completi + documentazione

**Tutto sarà operativo e conforme a norma entro un mese!** 🚀