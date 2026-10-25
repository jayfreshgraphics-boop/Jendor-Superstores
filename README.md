# Jendor Superstores

Demo online store with a supplier portal, plus an n8n workflow that parses supplier price and stock events, logs them to Baserow and sends formatted Telegram alerts. Malformed payloads are rejected with HTTP 400.

Designed by JayFresh Inc.

## Contents
- `index.html` – storefront and supplier portal (single file, no build step)
- `workflows/supplier-webhook-parser.json` – n8n workflow (import into n8n)

## Workflow setup
1. Import the JSON into n8n and add Telegram and Baserow credentials.
2. Set the Telegram chat ID, Baserow database ID and table ID.
3. Baserow columns: event_type, sku, supplier, product_name, old_value, new_value, change_pct, currency, severity, received_at, raw_payload.
4. In workflow settings, set Error Workflow to the workflow itself.
5. Activate it, then paste the production endpoint URL into the portal under Integration settings.
6. Allow your site origin in the n8n Webhook node (Allowed Origins).

## Event payloads
price_change: event_type, sku, supplier, old_price, new_price, currency (optional product_name)
stock_change: event_type, sku, supplier, old_stock, new_stock (optional product_name)

## Notes
The portal login is a front-end demo gate. Use a real auth backend (e.g. Supabase Auth) before production.
