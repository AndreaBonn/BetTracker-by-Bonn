<p align="center">
  <img src="assets/icon.png" alt="BetTracker" width="120" height="120" style="border-radius: 20px;" />
</p>

<h1 align="center">BetTracker</h1>

<p align="center">
  <strong>Track, analyze, and improve your sports betting performance.</strong><br/>
  A free Progressive Web App — no download required.
</p>

<p align="center">
  <a href="https://bettracker-bybonn.web.app">
    <img src="https://img.shields.io/badge/Open_App-BetTracker-10b981?style=for-the-badge&logo=googlechrome&logoColor=white" alt="Open BetTracker" />
  </a>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/React-18-61dafb?logo=react&logoColor=white" alt="React 18" />
  <img src="https://img.shields.io/badge/TypeScript-5.6-3178c6?logo=typescript&logoColor=white" alt="TypeScript" />
  <img src="https://img.shields.io/badge/Firebase-10-ffca28?logo=firebase&logoColor=black" alt="Firebase" />
  <img src="https://img.shields.io/badge/Tailwind_CSS-3-06b6d4?logo=tailwindcss&logoColor=white" alt="Tailwind CSS" />
  <img src="https://img.shields.io/badge/PWA-Installable-5a0fc8?logo=pwa&logoColor=white" alt="PWA" />
</p>

<p align="center">
  <a href="README.it.md">Italiano</a> · <a href="SECURITY.md">Security</a>
</p>

---

## What is BetTracker?

BetTracker is a personal sports betting tracker designed to help you **understand your betting habits** through data. It doesn't encourage gambling — it gives you a clear, honest picture of your results so you can make informed decisions.

Whether you bet for real or just want to simulate without risking money, BetTracker keeps everything organized in one place: your bet slips, your bookmaker balances, your performance stats, and AI-powered analysis.

---

## Features

### New Bet Slip
Create single or accumulator bets with full details: teams, sport, competition, bet type, odds, stake, and bookmaker. Choose between **Real** (actual money) and **Virtual** (simulation) mode.

### Screenshot Import (AI-powered)
Snap a photo of your bet slip from any bookmaker app. BetTracker uses **Gemini AI** to automatically extract all matches, odds, stake, and bookmaker name — saving you manual entry time.

### History
Browse all your bet slips with filters by status (Won / Lost / Pending), mode (Real / Virtual), and bookmaker. Update outcomes, record actual winnings, or share slips with friends via a unique public link.

### Statistics
Three dedicated tabs give you a complete performance overview:

| Tab | What it shows |
|-----|---------------|
| **Balance** | Current balance per bookmaker, total P&L, deposit/withdrawal history |
| **Statistics** | Total bets, win rate, ROI, invested vs won, bankroll trend chart, odds distribution chart |
| **Insights** | Performance by odds range, single vs accumulator comparison, 7/30-day rolling profit chart, best & worst bets, win/loss streaks, expected vs actual win rate |

### AI Chat Assistant
Ask questions about your data in natural language. Powered by **Gemini 2.5 Flash**, the assistant analyzes your real betting history and provides insights like:
- *"How am I performing on football vs basketball?"*
- *"What's my ROI on accumulators above 3.00 odds?"*
- *"Compare my results across bookmakers"*

The AI is restricted to your data analysis only — it will never give betting tips or predictions.

### Share Bet Slips
Generate a shareable public link for any bet slip. Friends can view match details, odds, and results without needing an account. A visit counter tracks how many people have seen it.

### Settings
- **Profile**: Google account info and logout
- **Gemini API Key**: Configure your free key for AI features (screenshot import + chat)
- **Notifications**: Push notification toggle
- **Preferences**: Currency (EUR/USD/GBP), auto-refresh results
- **Language**: English and Italian with automatic browser detection
- **Data Management**: Export to CSV or Excel, import from CSV, full JSON backup & restore, archive old slips
- **Account Deletion**: Permanently delete all data with double confirmation

---

## How to Use It

### 1. Sign In
Open [bettracker-bybonn.web.app](https://bettracker-bybonn.web.app) and sign in with your Google account. That's it — no registration form, no email verification.

### 2. Set Up Your AI Key (Optional)
Go to **Settings** and paste your free Gemini API key (get one at [aistudio.google.com](https://aistudio.google.com)). This unlocks the screenshot import feature and the AI chat assistant.

### 3. Add Your First Bet Slip
- Tap **New Bet Slip**
- Choose **Real** or **Virtual** mode
- Add one or more matches with sport, teams, bet type, and odds
- Enter your stake and bookmaker
- Save — done!

Alternatively, use **Import from Photo** to let AI read your bookmaker's screenshot.

### 4. Track Your Results
When a bet resolves, go to **History**, update its status (Won/Lost), and enter the actual payout. Your stats and balance update automatically.

### 5. Manage Your Bankroll
In **Statistics > Balance**, register deposits and withdrawals for each bookmaker. BetTracker calculates your net profit per bookmaker and overall.

### 6. Analyze Your Performance
Check **Statistics** and **Insights** to understand where you win, where you lose, and how your strategy evolves over time.

### 7. Install as App (Optional)
BetTracker is a PWA — on mobile, tap "Add to Home Screen" for a native app experience. It works offline for browsing your data.

---

## Requirements

| Requirement | Details |
|-------------|---------|
| **Browser** | Any modern browser (Chrome, Safari, Firefox, Edge) |
| **Account** | Google account for authentication |
| **AI Features** | Free Gemini API key ([get one here](https://aistudio.google.com)) |
| **Cost** | Completely free |

---

## Tech Stack

BetTracker is a modern single-page application built with production-grade tools:

| Layer | Technology |
|-------|------------|
| **Frontend** | React 18, TypeScript 5.6, Vite 6 |
| **Styling** | Tailwind CSS 3, shadcn/ui components, Lucide icons |
| **State** | Zustand (global), React Query (server state) |
| **Backend** | Firebase Authentication (Google OAuth), Cloud Firestore (database), Firebase Hosting |
| **AI** | Google Gemini 2.5 Flash (chat + vision OCR) |
| **Charts** | Recharts |
| **Forms** | React Hook Form + Zod validation |
| **i18n** | i18next with browser language detection |
| **PWA** | vite-plugin-pwa, Service Worker, offline support |
| **Data Export** | CSV, XLSX (SheetJS), JSON backup/restore |

### Architecture Highlights
- **Mobile-first responsive design** with dark theme
- **Row-level security** via Firestore rules — users can only access their own data
- **Client-side key storage** — Gemini API keys are stored in the user's Firestore profile, never exposed to other users
- **Offline-capable** — IndexedDB caching via `idb` for seamless offline browsing
- **Zero backend code** — fully serverless architecture on Firebase

---

## Privacy & Security

Your data is yours. BetTracker stores everything in your personal Firebase account, protected by Google authentication and Firestore security rules. No one — including the developer — can access your betting data.

For full details, see the [Security Policy](SECURITY.md).

---

## License

This project is released under a [custom license](LICENSE) — the app is free to use for personal purposes.

---

## Author

**Andrea Bonacci** — [GitHub](https://github.com/AndreaBonn)

---

<p align="center">
  <sub>BetTracker does not encourage gambling. It is a personal tracking tool. Bet responsibly.</sub>
</p>
