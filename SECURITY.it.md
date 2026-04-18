# Policy di Sicurezza

<p align="right">
  <a href="SECURITY.md">English</a> · <a href="README.it.md">Torna al README</a>
</p>

BetTracker è progettato con la privacy e la sicurezza dei tuoi dati come priorità assoluta. Questo documento spiega le misure tecniche adottate per proteggere le tue informazioni.

---

## Autenticazione

- **Google OAuth 2.0** — BetTracker usa Firebase Authentication con Google come unico provider di identità. Non gestiamo, memorizziamo o vediamo mai la tua password.
- **Nessuna credenziale personalizzata** — Non ci sono username, email o password salvate nel database dell'applicazione. L'autenticazione è interamente delegata all'infrastruttura sicura di Google.
- **Gestione sessioni** — I token di autenticazione sono gestiti dal Firebase SDK con refresh automatico e salvataggio sicuro nel browser.

## Isolamento dei Dati

Ogni dato che crei in BetTracker è legato al tuo ID utente unico e protetto da **Regole di Sicurezza Firestore lato server**:

```
match /schedine/{id} {
  allow read, update, delete: if request.auth.uid == resource.data.userId;
  allow create: if request.auth.uid == request.resource.data.userId;
}
```

Questo significa:
- Puoi **solo leggere, modificare e cancellare i tuoi dati** — questo viene applicato a livello di database, non solo nel codice dell'app.
- Anche se qualcuno creasse una richiesta API malevola, Firebase rifiuterebbe qualsiasi tentativo di accedere ai record di un altro utente.
- Le stesse regole si applicano al tuo profilo, alle schedine e alle transazioni finanziarie.

## Schedine Condivise

Quando condividi una schedina, viene creato uno **snapshot di sola lettura** in una collezione pubblica separata. Questo snapshot:
- Contiene solo dettagli delle partite, quote, importo e stato — nessuna informazione personale.
- È accessibile tramite un ID unico e non indovinabile.
- Può essere creato o eliminato solo dal proprietario originale.
- L'unico campo scrivibile pubblicamente è il contatore visite.

## Sicurezza Chiave API

Le funzionalità AI di BetTracker (importazione screenshot e chat) richiedono una chiave API Gemini personale. Ecco come viene gestita:

- **La tua chiave, il tuo controllo** — La chiave API è salvata nel tuo documento profilo personale su Firestore, protetta dalle stesse regole di isolamento utente descritte sopra.
- **Nessun relay server** — Le chiamate API a Gemini vengono fatte direttamente dal tuo browser all'API di Google. I server di BetTracker non vedono, registrano o fanno da proxy alla tua chiave.
- **Nessun altro utente può accedervi** — Le regole Firestore assicurano che solo tu puoi leggere il tuo documento profilo.
- **Puoi rimuoverla in qualsiasi momento** — Cancella la tua chiave dalle Impostazioni ed è rimossa immediatamente.

## Archiviazione dei Dati

| Dato | Dove | Accesso |
|------|------|---------|
| Schedine | Cloud Firestore | Solo il tuo account autenticato |
| Saldi bookmaker | Cloud Firestore | Solo il tuo account autenticato |
| Transazioni finanziarie | Cloud Firestore | Solo il tuo account autenticato |
| Profilo utente + chiave API | Cloud Firestore | Solo il tuo account autenticato |
| Schedine condivise | Cloud Firestore | Lettura pubblica (solo snapshot) |
| Cache offline | IndexedDB (tuo browser) | Solo dispositivo locale |

## Cosa NON Facciamo

- **Non** raccogliamo analytics o telemetria di utilizzo.
- **Non** usiamo script di tracciamento di terze parti (niente Google Analytics, niente Meta Pixel, niente cookie).
- **Non** vendiamo, condividiamo o elaboriamo i tuoi dati per scopi diversi dal funzionamento dell'app.
- **Non** abbiamo un backend server-side — BetTracker è un'applicazione puramente client-side che comunica direttamente con Firebase e l'API Gemini.
- **Non** salviamo dati al di fuori del tuo account Firebase.

## Eliminazione Account

Hai il pieno controllo sui tuoi dati:

1. Vai in **Impostazioni > Zona Pericolosa**.
2. Clicca **Elimina Account** — una doppia conferma previene cancellazioni accidentali.
3. Tutti i tuoi dati vengono rimossi permanentemente da Firestore: schedine, transazioni, profilo e schedine condivise.
4. Il tuo account Firebase Authentication viene eliminato.
5. Questa azione è irreversibile.

## Portabilità dei Dati

Prima di eliminare il tuo account, puoi esportare tutti i tuoi dati:

- **Export CSV** — File piatto con tutte le schedine.
- **Export Excel** — Foglio di calcolo formattato con tutte le schedine.
- **Backup JSON completo** — Dump completo di schedine e transazioni, reimportabile in BetTracker.

## Infrastruttura

BetTracker gira interamente sull'infrastruttura **Google Cloud** tramite Firebase:

- **Firebase Hosting** — Sito statico servito tramite HTTPS con certificati SSL automatici.
- **Cloud Firestore** — Database NoSQL gestito con regole di sicurezza lato server, backup automatici e crittografia a riposo.
- **Firebase Authentication** — Implementazione OAuth 2.0 standard di settore.

Tutti i dati in transito sono crittografati tramite **TLS 1.3**. Tutti i dati a riposo sono crittografati dalla crittografia predefinita di Google Cloud.

## Segnalare una Vulnerabilità

Se scopri una vulnerabilità di sicurezza, segnalala in modo responsabile:

- **Email**: Contatta l'autore tramite [GitHub](https://github.com/AndreaBonn)
- **Non** aprire una issue pubblica per vulnerabilità di sicurezza.

---

<p align="center">
  <sub>Ultimo aggiornamento: aprile 2026</sub>
</p>
