# Carrier Factoring Prequalification Engine & Warm Handoff Architecture

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Automation: n8n](https://img.shields.io/badge/Workflow-n8n-EA4B71.svg)](https://n8n.io)
[![Stack: Tailwind CSS](https://img.shields.io/badge/Frontend-TailwindCSS-38B2AC.svg)](https://tailwindcss.com)
[![Status: Production Live](https://img.shields.io/badge/Status-Production%20Live-success.svg)](https://www.dispatch.businessautomationempire.com/carrier-factoring-prequalification-engine/)

An intelligent, mobile-first, 45-second micro-prequalification engine and automated lead routing workflow built for freight dispatchers, freight brokers, and trucking affiliate marketers. 

Designed to convert cold trucker outreach (e.g. 10,000+ carrier email lists) into high-intent factoring accounts by prequalifying carriers dynamically and routing them to the optimal funding partner while protecting 10% lifetime partner commissions.

---

## 🌐 Live Production Demo

- **Live Page:** [https://www.dispatch.businessautomationempire.com/carrier-factoring-prequalification-engine/](https://www.dispatch.businessautomationempire.com/carrier-factoring-prequalification-engine/)
- **Target Audience:** Owner-Operators, Independent Fleet Owners, Freight Dispatchers, Factoring Brokers

---

## ⚡ The Problem: Why Cold Factoring Outreach Fails

Most freight dispatchers and affiliate marketers fail when emailing carriers about factoring because they commit one of two fatal mistakes:

1. **Directly Dumping Leads on Bank Reps:** Traditional factoring desks (like Summar Financial) require authorities older than 90 days and regular monthly billing ($10,000+/mo). Submitting unvetted carriers leads to high rejection rates, frustrated underwriting reps, and lost trust.
2. **Pushing 1-Year Predatory Contracts to Contract-Phobic Drivers:** Many truckers have been burned by restrictive 1-to-2 year factoring contracts with harsh minimum monthly volume penalties. Forcing them into traditional factoring produces high drop-off.
3. **Attribution Loss:** Sending cold leads to generic corporate sign-up pages causes referrers to lose their **10% lifetime recurring commission** or partner bounties.

---

## 🚀 The Solution: Dual-Tier Dynamic Routing

This system uses a **45-second 4-question intake form** connected via real-time webhooks to an intelligent **n8n automation router**:

```
+-------------------------------------------------------------------------------+
|                      10,000 COLD TRUCKER OUTREACH                             |
+-------------------------------------------------------------------------------+
                                      |
                                      v
       [ 45-Second Micro-Prequalification Engine (4 Questions) ]
                                      |
                   +------------------+------------------+
                   |                                     |
                   v                                     v
       [ Authority > 90 Days ]               [ Authority < 90 Days OR ]
       [ Gross > $10k/month  ]               [ Gross < $10k/month  OR ]
       [ Full Fleet Factor   ]               [ Contract-Averse Spot   ]
                   |                                     |
                   v                                     v
     +--------------------------+          +--------------------------+
     |   SUMMAR FINANCIAL       |          |      BASICBLOCK          |
     | Rep: Elizabeth Valencia  |          | Rep: Sydney Lock         |
     | - True Non-Recourse      |          | - 2.5% Flat Rate         |
     | - Same-Day Pay by 2PM    |          | - ZERO Lock-In Contracts |
     | - Load Connex Fuel Card  |          | - $5 Same-Day RTP        |
     | - 10% Lifetime RevShare  |          | - Flat Referral Bounty   |
     +--------------------------+          +--------------------------+
                   |                                     |
                   v                                     v
       [ Automated Warm Intro ]              [ Instant Link & Email ]
       [ & HubSpot Calendar   ]              [ with Priority Token  ]
```

### 1. Tier 1: Summar Financial (High-Volume & Non-Recourse Protection)
- **Qualified Criteria:** Authority $\ge 90$ days, Monthly Gross $\ge \$10,000$, Standard equipment (Dry Van, Reefer, Flatbed, Box Truck).
- **Driver Benefits:** True non-recourse credit default protection (Summar Shield), same-day ACH funding before 2:00 PM EST, Load Connex diesel discount cards.
- **Warm Handoff:** Automated warm introduction email dispatched directly from the Managing Director to Senior Account Executive **Elizabeth Valencia**, CC'ing the driver and referrer. Form renders a one-click direct booking link to Elizabeth's private HubSpot calendar.
- **Affiliate Attribution:** Locks in 10% lifetime recurring fee split.

### 2. Tier 2: BasicBlock (New Authorities & Zero-Contract Spot Factoring)
- **Qualified Criteria:** Authority $< 90$ days, Monthly Gross $<\$10,000$, or carriers explicitly requesting no contracts.
- **Driver Benefits:** Industry-leading **2.5% flat non-recourse rate**, zero long-term contracts, cancel anytime, $5 instant RTP payouts, and 50% fuel advances on rate confirmations.
- **Activation Flow:** Instant confirmation email dispatched to the driver with dedicated partner specialist **Sydney Lock**'s direct contact, plus immediate redirect to the 3-minute self-onboarding portal.

---

## 📂 Repository Structure

```
.
|-- README.md
|-- LICENSE
|-- frontend/
|   |-- index.html                    # Standalone responsive web application (ready for local / static deploy)
|   |-- wordpress-embed.html          # Clean snippet optimized for WordPress (Elementor, Gutenberg, Custom HTML)
|-- n8n/
|   |-- trucker-factoring-prequal-workflow.json  # Full n8n workflow export (ready to import)
|   |-- README.md                     # Step-by-step n8n deployment & Gmail OAuth configuration guide
|-- scripts/
|   |-- deploy_wp_page.py             # Programmatic WordPress deployment via Royal MCP / REST API
|   |-- deploy_n8n_workflow.py        # Programmatic workflow deployment via n8n REST API
|   |-- test_prequal_webhook.py       # End-to-end routing validation script
|-- docs/
|   |-- routing-logic.md              # Detailed algorithmic prequalification rules & edge cases
|   |-- cold-email-templates.md       # High-converting email copy for 10k carrier outreach
```

---

## 🛠️ Setup & Deployment Guide

### Prerequisites
- Node.js / Python 3.8+
- An [n8n](https://n8n.io) instance (Cloud or Self-Hosted) with Gmail OAuth2 configured
- A web host (WordPress, Netlify, Vercel, or GitHub Pages)

### 1. Import n8n Workflow
1. In your n8n dashboard, click **Workflows** > **Add Workflow** > **Import from File**.
2. Select `n8n/trucker-factoring-prequal-workflow.json`.
3. Open the two Gmail nodes (`Send Intro Email to Elizabeth (Summar)` and `Send BasicBlock Activation Email`) and connect your Gmail OAuth2 credential.
4. Activate the workflow and copy the **Production Webhook URL**:
   `https://<your-n8n-instance>/webhook/trucker-factoring-prequal`

### 2. Configure Frontend
1. Open `frontend/index.html` or `frontend/wordpress-embed.html`.
2. Replace `WEBHOOK_URL` in the `<script>` section with your live n8n webhook URL:
   ```javascript
   const WEBHOOK_URL = 'https://<your-n8n-instance>/webhook/trucker-factoring-prequal';
   ```
3. Deploy to your WordPress site or static hosting.

### 3. Test Routing
Run the test script to verify both routes are functioning:
```bash
python scripts/test_prequal_webhook.py --url https://<your-n8n-instance>/webhook/trucker-factoring-prequal
```

---

## 📧 Cold Email Campaign Playbook

Included in [`docs/cold-email-templates.md`](docs/cold-email-templates.md) are proven outreach sequences designed to drive cold truckers to the 45-second engine:
- High deliverability, plain-text format.
- Addresses high interest rates, broker payment lag (30-45 days), and predatory contracts.
- High conversion rate ($>12\%$ click-through on warm domain pools).

---

## 🔒 Security & Privacy Best Practices

- **Zero Hardcoded Secrets:** All API keys and tokens in scripts are parameterized via environment variables (`N8N_API_KEY`, `WP_AUTH_TOKEN`).
- **No Soft/Hard Credit Pulls:** Prequalification is purely operational (MC/DOT age, equipment, gross revenue). Driver credit score is never impacted during prequalification.
- **CORS Configured:** Webhook response node is configured with appropriate Access-Control headers to support cross-domain AJAX requests.

---

## 📄 License

Distributed under the MIT License. See `LICENSE` for more information.

---

**Developed & Maintained by:**  
[Empire Dispatch Logistics](https://www.dispatch.businessautomationempire.com/)  
Managing Director: Edward Ssewanyana  
Contact: dispatch@businessautomationempire.com | (782) 201-5130
