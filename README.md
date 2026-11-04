# Pinnora Black Box — Developer handoff

## What this includes
- `public/index.html`: updated listicle with Black Box challenge.
- `server.js`: Express backend; reads a public product webpage, sends extracted text to OpenAI for four **hypothetical** marketing directions; returns only one direction initially. When the user submits an email, sends a lead notification to your team using Resend and unlocks the remaining three.
- `.env.example`: required configuration.

## Setup
1. Install Node.js 20+, run `npm install`.
2. Configure these environment variables through your host or a local `.env` loader: `OPENAI_API_KEY`, `OPENAI_MODEL`, `RESEND_API_KEY`, `RESEND_FROM`, `LEADS_TO`, and optional `PORT`.
3. Verify the sending domain in Resend. The lead notification inbox is already configured as `LEADS_TO=manish.panchal@thepinnacle.media` in `.env.example`; copy this to your actual deployment environment.
4. Start with `npm start`. The listicle and backend must be served from the **same origin**. Visit `http://localhost:3000/`.
5. Submit a public product URL and then an email address. Confirm the destination email arrives before advertising the experience.

## Required before production
- Replace privacy notice link with the exact published Pinnora Privacy Policy and clearly disclose lead retention and contact usage. Don't subscribe users to marketing newsletters without separate consent.
- Server stores pending challenges in RAM for 20 minutes. Move to Redis or another TTL database for multi-instance deployment. This demo is not a production persistence layer.
- Add Turnstile/reCAPTCHA, account-level usage limits, monitoring, webhook/CRM integration, spam protection and audit logs with appropriate retention.
- Review SSRF protections with your infrastructure/security team. Hosted website fetches may be blocked by access controls, and JavaScript-rendered pages may not be readable. No competitor research is performed; the result is a grounded creative hypothesis based on publicly accessible website text.
- Ensure eligible advertiser categories and product claims comply with applicable platform policies.
- Use production error handling and ensure customer data is processed under your published privacy policy.

The HTML file alone cannot send emails or return real AI analysis. Do not publish a false 'lead sent' message when notification delivery fails.
