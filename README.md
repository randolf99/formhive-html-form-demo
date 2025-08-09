# formhive-html-form-demo
Beispielcode &amp; Demo: HTML-Formulare mit formhive.net verarbeiten – ohne eigenes Backend. Inklusive cURL, JavaScript und Zapier-Anbindung.

# formhive.net

> **Empfange Formular-Daten ohne eigenes Backend.**  
> Einfacher Endpoint, sofort einsatzbereit – mit E-Mail-Benachrichtigung, Webhooks, Zapier & Integrationen.  
> **Reine Formsache.**

## 🚀 Warum formhive?
- **Kein Backend nötig** – einfach Formular anlegen und Endpoint einfügen
- **E-Mail Alerts** – sofort benachrichtigt bei neuen Einreichungen
- **Automatisierungen** – Webhooks, Slack, Teams, Zapier & mehr
- **Teamfähig** – Projekte & Rechteverwaltung für Agenturen

---

## ⚡ Quick Start

### 1. Kostenlos registrieren
➡ [https://formhive.net](https://formhive.net)

### 2. Formular anlegen & Form-ID kopieren

### 3. HTML-Formular einbinden
```html
<form action="https://app.formhive.net/submit/<DEIN_FORM_ID>" method="POST">
  <input type="text" name="name" placeholder="Dein Name" required>
  <input type="email" name="email" placeholder="Deine E-Mail" required>
  <textarea name="message" placeholder="Nachricht" required></textarea>
  <button type="submit">Senden</button>
</form>
``
