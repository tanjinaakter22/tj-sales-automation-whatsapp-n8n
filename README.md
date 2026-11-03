# 🚀 TJ Sales Automation - WhatsApp AI Sales Chatbot

An automated, memory-enabled WhatsApp E-Commerce Sales Engine powered by **n8n**, **Meta WhatsApp Cloud API**, **Google Gemini 1.5 Flash**, and **Google Sheets**.

This system handles customer inquiries about product availability, prices, sizes, and colors, maintains conversational context across chat turns, and automatically captures confirmed orders directly into a Google Sheet database.

---

## 📸 Demo & Screenshots
<img width="576" height="1280" alt="6289838451351819794_121" src="https://github.com/user-attachments/assets/6c8a34ba-6e83-465a-be13-ad1f53442178" />
<img width="1366" height="768" alt="Screenshot (5)" src="https://github.com/user-attachments/assets/dbb741b7-3277-488d-89ac-477987b7152a" />
<img width="1366" height="768" alt="Screenshot (4)" src="https://github.com/user-attachments/assets/0e8ac6d5-22a5-455f-854c-7184725a799e" />
<img width="1366" height="768" alt="Screenshot (3)" src="https://github.com/user-attachments/assets/5c059da6-5857-4740-a1ac-938bf75c77cc" />



---

## 🌟 Key Features

* **🤖 Smart Product Catalog Inquiry:** AI Agent responds accurately to product queries (prices, sizes, colors, and stock status) based on a structured system catalog.
* **🧠 Conversation Memory:** Utilizes n8n's Simple Memory (Window Buffer Memory) with WhatsApp phone numbers as Session Keys to remember context across multi-turn chats.
* **📊 Automatic Order Logging:** Integrates a custom Google Sheets Tool that dynamically appends order details (*Customer Name, Phone, Address, Product, Quantity, Total Price, Order Status*) upon user confirmation.
* **⚡ Real-Time Webhook Trigger:** Connected directly via Meta Cloud API using permanent access tokens for instant message processing.

---

## 🛠️ Tech Stack & Prerequisites

* **Workflow Orchestration:** [n8n](https://n8n.io/)
* **AI Model:** Google Gemini 1.5 Flash (via Google AI Studio)
* **Messaging Platform:** Meta WhatsApp Cloud API
* **Database / Order Storage:** Google Sheets API
* **Deployment:** Cloud / Self-Hosted n8n Instance

---

## 📐 Workflow Architecture & Logic Flow

1. **Trigger:** `WhatsApp Trigger` receives customer messages via Meta Webhooks.
2. **Context & Memory:** Passes the incoming message and phone number session key to the `Simple Memory` node.
3. **AI Agent Processing:** `Google Gemini 1.5 Flash` evaluates user intent against the internal product catalog prompt:
   - If inquiring, provides dress details.
   - If ordering, collects missing customer details step-by-step.
4. **Tool Execution:** Once all details are gathered and confirmed by the user, the AI invokes the `Google Sheets Tool` (`create_order`).
5. **Data Persistence:** Automatically inserts a new row in Google Sheets with `Order Status: Confirmed`.
6. **Reply:** Sends a confirmation message back to the customer on WhatsApp.

---

## 📋 Product Catalog Configuration

The system prompt is configured with the following active catalog structure:

| ID | Product Name | Category | Price (BDT) | Sizes | Colors | Status |
|---|---|---|---|---|---|---|
| D101 | Cotton Three Piece | Three Piece | 1,200 | M, L, XL | Red, Blue | In Stock |
| D102 | Silk Saree | Saree | 2,500 | Free Size | Red, Green | In Stock |
| D103 | Designer Kurti | Kurti | 850 | S, M, L | Yellow | Out of Stock |
| D104 | Anarkali Dress | Gown | 3,200 | L, XL | As Specified | In Stock |

---

## ⚙️ Google Sheets Integration Schema

The Google Sheets node maps AI parameters to the following column headers:

* `Customer's name`
* `Phone`
* `Address`
* `Products`
* `Quantity`
* `Total price`
* `Order Status` *(Automatically set to "Confirmed")*

---

## 🚀 How to Import and Run

1. Clone this repository or copy the workflow JSON file.
2. In your **n8n** instance, create a new workflow and click **Import from File / Paste JSON**.
3. Configure your credentials for:
   - Meta WhatsApp Cloud API / WhatsApp Trigger
   - Google Gemini API Key
   - Google Sheets OAuth / Service Account
4. Ensure the Google Sheet document ID and sheet name are correctly mapped in the Google Sheets Tool node.
5. Save and set the workflow status to **Active**.

---

## 👤 Author

