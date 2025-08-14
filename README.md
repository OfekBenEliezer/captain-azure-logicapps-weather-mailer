@"
# Azure Logic Apps - Weather to Email

A clean Logic App that receives a city and an email, fetches live weather from OpenWeather, and sends a formatted email via Office 365.

## What it does
- HTTP trigger receives:
  ```json
  { "city": "Tel Aviv", "email": "user@example.com" }
