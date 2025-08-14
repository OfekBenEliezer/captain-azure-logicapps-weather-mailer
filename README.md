````markdown
# 🌤 Azure Logic Apps - Weather to Email

**Weather Mailer** is a clean, ready-to-deploy **Azure Logic App** that takes a city name and an email address, fetches live weather data from [OpenWeather](https://openweathermap.org/api), and sends a well-formatted email using Office 365.

---

## 🚀 What it does
1. **HTTP Trigger** receives a JSON payload:
   ```json
   { "city": "Tel Aviv", "email": "user@example.com" }
````

2. **Calls the OpenWeather API** to get the latest weather in metric units (°C).
3. **Parses and processes** the response - extracting temperature, feels-like temperature, humidity, wind speed, and weather description.
4. **Converts wind speed** from m/s to km/h.
5. **Sends a formatted email** through Office 365 containing all the relevant weather details.

---
## 🧭 Architecture
```mermaid
flowchart LR
  A[Client or Caller] -->|HTTP POST JSON (city, email)| B[Logic App - HTTP Trigger]
  B --> C[HTTP action - OpenWeather API]
  C -->|JSON weather data| D[Parse JSON]
  D --> E[Compose values: temp, feels_like, humidity, wind m/s -> km/h]
  E --> F[Office 365 - Send an email]
  F --> G[Recipient inbox]


```markdown
## Sequence
```mermaid
sequenceDiagram
  autonumber
  participant Client
  participant LogicApp as Logic App
  participant OpenWeather as OpenWeather API
  participant O365 as Office 365

  Client->>LogicApp: HTTP POST (city, email)
  LogicApp->>OpenWeather: GET /data/2.5/weather?q=<city>&units=metric
  OpenWeather-->>LogicApp: 200 OK (JSON)
  LogicApp->>LogicApp: Parse JSON + convert wind m/s -> km/h
  LogicApp->>O365: Send email (HTML body)
  O365-->>Client: Email delivered

  Client->>LogicApp: HTTP POST { city, email }
  LogicApp->>OpenWeather: GET /data/2.5/weather?q=<city>&units=metric
  OpenWeather-->>LogicApp: 200 OK (JSON)
  LogicApp->>LogicApp: Parse JSON and convert wind m/s → km/h
  LogicApp->>O365: Send email (HTML body)
  O365-->>Client: Email delivered

  classDef azure fill:#2563eb,stroke:#1e40af,stroke-width:1,color:#fff
  classDef svc fill:#0ea5e9,stroke:#0369a1,stroke-width:1,color:#fff
  class B,D,E azure
  class C,F svc


## 🗂 Repository Structure

```
deploy/
 ├─ azuredeploy.json             # ARM template for deploying the Logic App and connections
 ├─ azuredeploy.parameters.json  # Example parameter file
workflow/
 └─ logicapp.definition.json     # Full Logic App workflow definition
docs/
 └─ screenshots / diagrams       # Documentation and images (optional)
```

---

## 📦 Deploy to Azure

Click below to deploy directly to your Azure subscription:

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FOfekBenEliezer%2Fcaptain-azure-logicapps-weather-mailer%2Fmain%2Fdeploy%2Fazuredeploy.json)

---

## ⚙ Prerequisites

* An active Azure subscription with permissions to deploy resources
* An [OpenWeather API key](https://home.openweathermap.org/users/sign_up) (free tier available)
* An Office 365 account with email sending permissions (Microsoft 365 Business Standard / E3 / E5 or equivalent)

---

## 🛠 How to use after deployment

1. Go to your deployed Logic App in the Azure Portal.
2. Open the **HTTP Trigger** step and copy the **HTTP POST URL**.
3. Send a POST request to the URL with the following JSON payload:

   ```json
   {
     "city": "London",
     "email": "you@example.com"
   }
   ```
4. Check your inbox - you should receive a nicely formatted weather report.

---

## 📌 Example Email Output

| Parameter   | Example Value |
| ----------- | ------------- |
| City        | Tel Aviv      |
| Temperature | 28°C          |
| Feels Like  | 30°C          |
| Humidity    | 60%           |
| Wind Speed  | 14 km/h       |
| Description | Clear sky     |

---

## ✨ Credits

Developed by **[Captain Azure - Ofek Ben Eliezer](https://github.com/OfekBenEliezer)**
Microsoft Certified Trainer | Azure Architect | AI & Cloud Expert

```
