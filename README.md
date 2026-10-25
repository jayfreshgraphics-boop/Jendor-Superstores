# Jendor Superstores

Demo online store with a supplier portal, plus an n8n workflow that parses supplier events (price change, stock change, new product, discount started/ended), logs them to Baserow and sends formatted Telegram alerts. Malformed payloads are rejected with HTTP 400.

Designed by JayFresh Inc.

## Contents
- `index.html` – storefront and supplier portal (single file, no build step)
- `workflows/supplier-webhook-parser-v2.json` – n8n workflow (import into n8n)
- `workflows/supplier-events-baserow.csv` – import file for the Baserow log table

## Setup
1. Baserow: import the CSV as a table, set `old_value`, `new_value`, `change_pct` to Number and `raw_payload` to Long text.
2. n8n: import the workflow, add Telegram and Baserow credentials, set the chat ID, set Error Workflow to itself, then activate.
3. Confirm the production endpoint URL matches `DEFAULT_ENDPOINT` in `index.html`.
4. Host with GitHub Pages (Settings, Pages, deploy from `main` branch, root folder).

## Notes
The portal login is a front-end demo gate. Use a real auth backend (e.g. Supabase Auth) before production.
