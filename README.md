# ecommerce-order-csv-to-xml-json-converter

Convert raw Shopify, WooCommerce, and Stripe order exports (CSV or JSON) into normalized accounting JSON, CSV, or XML payloads with automatic subtotal, tax (VAT/GST), and gross revenue summaries.

🔗 **Get your free API key:** [E-Commerce & Accounting Format Converter on RapidAPI](YOUR_RAPIDAPI_LISTING_URL) *(100 free requests/month)*

## Endpoints
- **`POST /v1/normalize-orders`** — Standardizes messy order CSV/JSON columns and calculates net, tax, shipping, and gross totals.
- **`POST /v1/convert-format`** — Converts structured records cleanly between JSON, CSV, and XML for ERP, Tally, or QuickBooks imports.

## Quick Start (Python)

```python
import requests

url = "https://YOUR_RAPIDAPI_HOST/v1/normalize-orders"

payload = {
"csv_data": "order_id,date,customer_email,subtotal,tax,shipping,currency\nORD-1001,2026-11-15,buyer@example.com,120.00,12.00,5.00,USD",
"default_tax_rate": 0.0
}

headers = {
"content-type": "application/json",
"x-rapidapi-key": "YOUR_RAPIDAPI_KEY",
"x-rapidapi-host": "YOUR_RAPIDAPI_HOST"
}

response = requests.post(url, json=payload, headers=headers)
print(response.json())
```

## Sample Response

```json
{
"summary": {
"order_count": 1,
"total_net_sales": 120.0,
"total_tax_collected": 12.0,
"total_gross_revenue": 137.0
},
"accounting_entries": [
{
"order_id": "ORD-1001",
"date": "2026-11-15",
"customer_email": "buyer@example.com",
"currency": "USD",
"net_subtotal": 120.0,
"tax_amount": 12.0,
"shipping_amount": 5.0,
"gross_total": 137.0
}
]
}
```
