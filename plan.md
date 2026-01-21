# Finance Email Tracker Plan

## Goal
Build a web app that reads only Gmail emails, uses AI to categorize them, extracts finance fields (amount, date, merchant, currency, tax, invoice #), stores data locally on the PC, shows a transactions table, and supports on-demand CSV/Excel export. The app must include two modes: Connect Gmail and Manual Entry. For now, use 20 static sample emails with the same workflow as real Gmail ingestion.

## Core Features (MVP)
- Connect to Gmail (future-ready)
- Manual email entry
- AI classification (finance / non-finance)
- AI extraction (finance only)
  - amount, date, merchant, currency, tax, invoice #
- Local data storage (SQLite)
- Transactions table UI
- Export CSV / Excel on-demand
- Use 20 sample emails (static JSON)

## Recommended Tech Stack
- Frontend: React + Tailwind CSS
- Backend: Python FastAPI
- Database (Local PC): SQLite
- AI: OpenAI API or local LLM
- Gmail integration (later): Google OAuth + Gmail API

## Database Schema (Local SQLite)

### Table: emails
- id (PK)
- subject
- sender
- body
- received_date
- category (finance / non-finance)
- confidence
- source (sample/gmail/manual)

### Table: transactions
- id (PK)
- email_id (FK)
- amount
- currency
- date
- merchant
- tax
- invoice_number
- verified (bool)

## End-to-End Workflow (Real Email Pipeline)

### Email ingestion
- For now: load 20 static emails from JSON
- Later: Gmail API fetch

### AI classification
- Label as finance / non-finance + confidence

### AI extraction
- Only for finance emails
- Extract amount, currency, date, merchant, tax, invoice #

### Storage
- Save email + extracted transaction to SQLite

### UI
- Transactions table + filters
- Manual edit support

### Export
- CSV/Excel download button

## Two Modes (Required)

### Mode 1: Connect Gmail
- OAuth login
- Fetch Gmail inbox
- Same AI pipeline

### Mode 2: Manual entry
- User pastes email text
- Same AI pipeline

## Sample Data (20 Emails)
Create `sample_emails.json`:
- 12 finance emails (invoices, receipts, bank alerts, subscriptions)
- 8 non-finance emails (marketing, personal, newsletters)
- Each finance email includes: amount, currency, date, merchant, tax, invoice #

## AI Prompting (Example)

### Classification prompt
```
You are a finance email classifier.
Return only: finance or non-finance.
Email: {subject + body}
```

### Extraction prompt
```
Extract these fields: amount, currency, date, merchant, tax, invoice_number.
Return JSON.
Email: {subject + body}
```

## UI Pages
- Dashboard (total finance emails, total amount)
- Emails table (filter by category)
- Transactions table (editable rows)
- Manual entry form
- Export page

## Development Phases

### Phase 1 (Now)
- Setup project
- Load 20 static emails
- AI classify + extract
- Store in SQLite
- Transactions table
- CSV/Excel export

### Phase 2 (Later)
- Gmail OAuth
- Fetch real Gmail emails
- Same pipeline
