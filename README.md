# 🌤 Azure Logic Apps - Weather to Email

**Weather Mailer** is a clean, ready-to-deploy **Azure Logic App** that takes a city name and an email address, fetches live weather data from [OpenWeather](https://openweathermap.org/api), and sends a well-formatted email using Office 365.

---

## 🚀 What it does
1. **HTTP Trigger** receives a JSON payload:
   ```json
   { "city": "Tel Aviv", "email": "user@example.com" }
Calls the OpenWeather API to get the latest weather in metric units (°C).

Parses and processes the response - extracting temperature, feels-like temperature, humidity, wind speed, and weather description.

Converts wind speed from m/s to km/h.

Sends a formatted email through Office 365 containing all the relevant weather details.

flowchart LR
    A[Client / Caller] -->|HTTP POST JSON<br/>{ city, email }| B[Logic App<br/>HTTP Trigger]
    B --> C[HTTP Action<br/>OpenWeather API]
    C -->|JSON weather data| D[Parse JSON]
    D --> E[Compose values<br/>temp, feels_like, humidity,<br/>wind(m/s) → km/h]
    E --> F[Office 365<br/>Send an email]
    F --> G[Recipient Inbox]

    classDef azure fill:#2563eb,stroke:#1e40af,stroke-width:1,color:#fff
    classDef svc fill:#0ea5e9,stroke:#0369a1,stroke-width:1,color:#fff
    class B,D,E azure
    class C,F svc


🗂 Repository Structure

deploy/
 ├─ azuredeploy.json             # ARM template for deploying the Logic App and connections
 ├─ azuredeploy.parameters.json  # Example parameter file
workflow/
 └─ logicapp.definition.json     # Full Logic App workflow definition
docs/
 └─ screenshots / diagrams       # Documentation and images (optional)
📦 Deploy to Azure
Click below to deploy directly to your Azure subscription:


⚙ Prerequisites
An active Azure subscription with permissions to deploy resources

An OpenWeather API key (free tier available)

An Office 365 account with email sending permissions (Microsoft 365 Business Standard / E3 / E5 or equivalent)

🛠 How to use after deployment
Go to your deployed Logic App in the Azure Portal.

Open the HTTP Trigger step and copy the HTTP POST URL.

Send a POST request to the URL with the following JSON payload:

{
  "city": "London",
  "email": "you@example.com"
}
Check your inbox - you should receive a nicely formatted weather report.

📌 Example Email Output
Parameter	Example Value
City	Tel Aviv
Temperature	28°C
Feels Like	30°C
Humidity	60%
Wind Speed	14 km/h
Description	Clear sky

✨ Credits
Developed by Captain Azure - Ofek Ben Eliezer
Microsoft Certified Trainer | Azure Architect | AI & Cloud Expert
