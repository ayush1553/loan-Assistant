# AI Loan Assistant – Personalized Conversational Loan Advisor

A demo web app that simulates an agentic AI flow for personal loans: sales → KYC verification → underwriting → sanction letter generation.

## Tech Stack
- Frontend: Static HTML/CSS/JS
- Backend: Node.js + Express
- PDF: pdfkit

## Project Structure
```
backend/
  package.json
  src/
    index.js
    routes/
      masterAgent.js
      pdf.js
    services/
      masterAgent.js
      workers/
        salesAgent.js
        verificationAgent.js
        underwritingAgent.js
        sanctionLetterAgent.js
    store/
      customers.js
      offers.js
frontend/
  index.html
  styles.css
  main.js
```

## Setup & Run
1. Open a terminal in `backend/` and install deps:
   ```bash
   npm install
   ```
2. Start the server:
   ```bash
   npm run start
   ```
3. Open the app at `http://localhost:3000`.

The frontend is served statically by the backend.

## Using the Demo
- The chat greets you. Try: `I need a personal loan`.
- Provide amount and tenure, e.g.: `₹100000 for 12 months`.
- Prefilled context uses a mock customer: `Ayush Prajapati, Varanasi, 9876543210` (editable by changing `window.__context` in `frontend/index.html`).
- If approved, a sanction letter PDF link appears.

## Business Rules
- Approved: credit score ≥ 700 and requested amount ≤ pre-approved limit.
- Pending: credit score ≥ 700 and amount ≤ 2× pre-approved limit → asks for salary slip.
- Rejected: credit score < 700 or amount > 2× pre-approved limit.

## Test Scenarios
- Case 1 – Approved:
  - Use `Ayush Prajapati, Varanasi, 9876543210` with `₹80,000` and `12 months`.
- Case 2 – Pending:
  - Use `₹150,000` and `12 months` for a customer with `preApprovedLimit` ≤ 100,000.
- Case 3 – Rejected:
  - Use a customer with credit score 650 (e.g., modify `customers.js` or rely on mock score if not verified).

## Notes
- Data is mock; no external APIs are called.
- PDFs are written to `backend/tmp` and served via `/pdf/:id`.
- This is a demo; do not use in production without security hardening.
