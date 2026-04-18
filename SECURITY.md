# Security Policy

<p align="right">
  <a href="SECURITY.it.md">Italiano</a> · <a href="README.md">Back to README</a>
</p>

BetTracker is designed with your privacy and data security as a top priority. This document explains the technical measures in place to protect your information.

---

## Authentication

- **Google OAuth 2.0** — BetTracker uses Firebase Authentication with Google as the sole identity provider. We never handle, store, or even see your password.
- **No custom credentials** — There are no usernames, emails, or passwords stored in the application database. Authentication is entirely delegated to Google's secure infrastructure.
- **Session management** — Authentication tokens are managed by the Firebase SDK with automatic refresh and secure storage in the browser.

## Data Isolation

Every piece of data you create in BetTracker is tied to your unique user ID and protected by **server-side Firestore Security Rules**:

```
match /schedine/{id} {
  allow read, update, delete: if request.auth.uid == resource.data.userId;
  allow create: if request.auth.uid == request.resource.data.userId;
}
```

This means:
- You can **only read, modify, and delete your own data** — this is enforced at the database level, not just in the app code.
- Even if someone crafted a malicious API request, Firebase would reject any attempt to access another user's records.
- The same rules apply to your profile, bet slips, and financial transactions.

## Shared Bet Slips

When you share a bet slip, a **read-only snapshot** is created in a separate public collection. This snapshot:
- Contains only match details, odds, stake, and status — no personal information.
- Is accessible via a unique, non-guessable ID.
- Can only be created or deleted by the original owner.
- The only field publicly writable is the visit counter.

## API Key Security

BetTracker's AI features (screenshot import and chat) require a personal Gemini API key. Here's how it's handled:

- **Your key, your control** — The API key is stored in your personal Firestore profile document, protected by the same user-isolation rules described above.
- **No server relay** — API calls to Gemini are made directly from your browser to Google's API. BetTracker's servers never see, log, or proxy your key.
- **No other user can access it** — Firestore rules ensure only you can read your profile document.
- **You can remove it anytime** — Delete your key from Settings and it's gone immediately.

## Data Storage

| Data | Where | Access |
|------|-------|--------|
| Bet slips | Cloud Firestore | Only your authenticated account |
| Bookmaker balances | Cloud Firestore | Only your authenticated account |
| Financial transactions | Cloud Firestore | Only your authenticated account |
| User profile + API key | Cloud Firestore | Only your authenticated account |
| Shared bet slips | Cloud Firestore | Public read (snapshot only) |
| Offline cache | IndexedDB (your browser) | Local device only |

## What We Don't Do

- We **don't** collect analytics or usage telemetry.
- We **don't** use third-party tracking scripts (no Google Analytics, no Meta Pixel, no cookies).
- We **don't** sell, share, or process your data for any purpose beyond the app's functionality.
- We **don't** have a server-side backend — BetTracker is a purely client-side application that communicates directly with Firebase and the Gemini API.
- We **don't** store any data outside of your Firebase account.

## Account Deletion

You have full control over your data:

1. Go to **Settings > Danger Zone**.
2. Click **Delete Account** — a double confirmation dialog prevents accidental deletion.
3. All your data is permanently removed from Firestore: bet slips, transactions, profile, and shared slips.
4. Your Firebase Authentication account is deleted.
5. This action is irreversible.

## Data Portability

Before deleting your account, you can export all your data:

- **CSV export** — Flat file with all bet slips.
- **Excel export** — Formatted spreadsheet with all bet slips.
- **Full JSON backup** — Complete dump of bet slips and transactions, re-importable into BetTracker.

## Infrastructure

BetTracker runs entirely on **Google Cloud** infrastructure through Firebase:

- **Firebase Hosting** — Static site served over HTTPS with automatic SSL certificates.
- **Cloud Firestore** — Managed NoSQL database with server-side security rules, automatic backups, and encryption at rest.
- **Firebase Authentication** — Industry-standard OAuth 2.0 implementation.

All data in transit is encrypted via **TLS 1.3**. All data at rest is encrypted by Google Cloud's default encryption.

## Reporting a Vulnerability

If you discover a security vulnerability, please report it responsibly:

- **Email**: Contact the author via [GitHub](https://github.com/AndreaBonn)
- **Do not** open a public issue for security vulnerabilities.

---

<p align="center">
  <sub>Last updated: April 2026</sub>
</p>
