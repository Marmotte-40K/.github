# 🛡️ Progetto Sicurezza Web – OWASP

## 🎯 Obiettivo
Sviluppare un'applicazione web (backend + frontend) che implementi meccanismi di protezione contro l'esposizione di dati sensibili, seguendo le best practices moderne.

## Copertura OWASP TOP10
## 📊 Copertura OWASP Top 10 (2021)

| OWASP Top 10                              | Stato      | Note                                                      |
|-------------------------------------------|------------|-----------------------------------------------------------|
| A01 – Broken Access Control               | ⚪ Non trattato | Estendibile con RBAC/IDOR                                 |
| A02 – Cryptographic Failures              | 🟢 Coperto  | Hash password, cifratura simmetrica, cookie sicuri        |
| A03 – Injection                           | 🟡 Parziale | Si può estendere con query parametrizzate / escaping      |
| A04 – Insecure Design / Data Exposure     | 🟢 Coperto  | Obiettivo principale del progetto                          |
| A05 – Security Misconfiguration           | 🟡 Parziale | Logging, rate limit ok; mancano CSP/headers                |
| A06 – Vulnerable and Outdated Components  | ⚪ Non trattato | Aggiungibile via `npm audit` o `pip list --outdated`      |
| A07 – Identification and Authentication Failures | 🟢 Coperto  | Login sicuro, 2FA, gestione token                          |
| A08 – Software and Data Integrity Failures| 🟡 Parziale | Firma JWT, invalidazione sessioni migliorabile            |
| A09 – Security Logging and Monitoring Failures | 🟢 Coperto  | Logging completo + mascheramento + log remoto             |
| A10 – Server-Side Request Forgery (SSRF)  | ⚪ Non trattato | Rilevante solo se presenti chiamate server-server         |


---

## ✅ Requisiti funzionali

### 🔐 Registrazione e Login sicuri
- [ ] Le password devono essere **hashate con bcrypt** (se node) o simili
- [ ] Il confronto deve avvenire con `bcrypt.compare`
- [ ] I **tentativi di login falliti** devono essere loggati
- [ ] Implementare **rate limit** o **blocco temporaneo** dopo N tentativi falliti

---

### 📜 Logging & Gestione errori
- [ ] Loggare **tutte le request e response** (file / std output)
- [ ] Mostrare in output all’utente solo **messaggi d’errore generici**
- [ ] I dettagli degli errori vanno nei log (es. stack trace, ID utente, IP…)
- [ ] Mascherare nei log i dati sensibili (`password`, `token`, `iban`, ecc.)

---

### 🔐 Protezione dei dati nel database
- [ ] Le password devono essere **hashate**
- [ ] I dati sensibili (IBAN, codice fiscale, note mediche…) devono essere **criptati simmetricamente**
  - Es: `crypto`, `crypto-js`, `node-forge`, o simili

---

### 🧪 Autenticazione a due fattori (2FA)
- [ ] Aggiungere 2FA **al login** e **al cambio password**
- [ ] Supportare due metodi:
  - App come **Google Authenticator** (TOTP, es. con `speakeasy`)
  - Codice via **email o SMS** (mockato)

---

### 🪪 Gestione Token
- [ ] Usare JWT:
  - **Access token** a breve durata (15 minuti)
  - **Refresh token** a lunga durata (7 giorni)
- [ ] Gestione access e refresh token (endpoint di refresh token)

---

## 🔄 Funzionalità Extra (facoltative ma consigliate)
- [ ] Inviare email (mock) al login da dispositivo nuovo
- [ ] Implementare il **logout da tutti i dispositivi**
- [ ] Invalidate i refresh token in caso di reset password
- [ ] Salvare i token in **cookie** con:
  - `HttpOnly`
  - `Secure`
  - `SameSite=Strict`


---

## 🧱 Stack tecnologico consigliato

### Backend
- Node.js (Fastify o Express)
- Python (Flask o FastAPI o Django)
- C# (.NET Core)

### Database
- MySQL
- MongoDB
- ...

### Frontend
- React
- Vue

---

## 📦 Consegna

- Repository GitHub con:
  - Codice backend e frontend
  - Istruzioni chiare per far partire il progetto
- README con:
  - Spiegazione delle misure di sicurezza implementate
  - Come testare i meccanismi (es. 2FA, token, logging)

---

## 🧠 Suggerimento

> Non limitarti a “far funzionare” tutto: **dimostra di aver capito perché ogni protezione è importante.** Mostrare i rischi associati ai casi vulnerabili può dare punti bonus.
