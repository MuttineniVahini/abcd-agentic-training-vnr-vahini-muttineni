# 🧭 **TripMate.AI — WhatsApp-Based Travel Planner (n8n Workflow)**

## 📘 **Overview**
**TripMate.AI** is an intelligent, WhatsApp-powered travel assistant built using **n8n**, **Google Gemini AI**, and **Google Sheets**.  
It automatically plans personalized travel itineraries based on the user’s WhatsApp message — including destination, duration, and budget.

When a user sends a message like *“Plan a 3-day trip to Goa with ₹10,000”*, the workflow:
1. Reads the message from WhatsApp.  
2. Uses Gemini AI to generate a detailed travel plan.  
3. Logs the conversation and trip details to Google Sheets.  
4. Replies directly to the user on WhatsApp with a friendly, AI-generated trip itinerary.

---

## ⚙️ **Prerequisites**

Before importing this workflow, make sure you have:
- ✅ **n8n Cloud / Self-Hosted Instance**
- ✅ **Meta WhatsApp Cloud API**  
  - Create a WhatsApp Business App at [Meta for Developers](https://developers.facebook.com/apps)  
  - Get your **Phone Number ID**, **Access Token**, and set up webhook verification.
- ✅ **Google Gemini API Key** (via [Google AI Studio](https://aistudio.google.com))
- ✅ **Google Sheets Integration** connected to n8n  
- (Optional) CSV/Sheet of sample travel data for AI memory

---

## 🧩 **Workflow Components**

### 1️⃣ **Receive WhatsApp Message (Webhook Node)**
- **Purpose:** Receives incoming messages from WhatsApp Cloud API.  
- **Path:** `/whatsapp`
- **Method:** `POST`

### 2️⃣ **IF Node**
- **Logic:** Checks if the incoming message is valid text.  
- If **True** → Continues to extract message text.  
- If **False** → Ends flow silently.

### 3️⃣ **Extract Message (Code Node)**
- **Function:** Parses incoming payload to extract name, number, message, timestamp.

### 4️⃣ **Load Memory (Google Sheets Node)**
- **Purpose:** Fetches previous travel data or user preferences.  
- **Operation:** `Read`

### 5️⃣ **Build Gemini Prompt (Code Node)**
- Constructs a structured prompt for Gemini based on input (destination, budget, etc.).

### 6️⃣ **Google Gemini Chat Model**
- **Purpose:** Uses Gemini AI to generate travel plans.
- **Model:** `gemini-pro` or `gemini-flash`

### 7️⃣ **Travel Planner (Agent Node)**
- **Inputs:**
  - **Chat Model:** Google Gemini Chat Model  
  - **Memory:** Google Sheets or Simple Memory node  

### 8️⃣ **Parse Gemini Response (Code Node)**
- **Function:** Cleans and formats Gemini’s text output into structured JSON.

### 9️⃣ **Log Trip to Google Sheets**
- **Purpose:** Appends trip plan and message to Google Sheet.  

### 🔟 **Send Reply to WhatsApp (HTTP Node)**
- Sends itinerary back to user via WhatsApp Cloud API.

---

## 📊 **Google Sheet Example**

| NAME | NUMBER | MESSAGE | DESTINATION | BUDGET | DURATION | ITINERARY | TIMESTAMP |
|------|---------|----------|--------------|---------|-----------|------------|-----------|
| Vahini | +91XXXXXXXXXX | Plan 3-day Goa trip ₹10000 | Goa | ₹10000 | 3 days | Beaches, Fort Aguada, Local Food Tour | 03-11-2025 00:45 |

---

## 🧩 **Environment Variables**

| Variable | Description |
|-----------|--------------|
| `WHATSAPP_TOKEN` | Meta WhatsApp API access token |
| `GEMINI_API_KEY` | Google Gemini API key |
| `SHEET_ID` | Google Sheet ID for storing travel data |

---

## 🚀 **Setup Steps**

1. **Import Workflow** → Upload JSON file to n8n.  
2. **Configure Credentials** → WhatsApp, Sheets, Gemini.  
3. **Deploy Webhook** → Paste URL in WhatsApp Developer Console.  
4. **Test** → Send a WhatsApp message like *“Plan a 2-day trip to Jaipur with ₹5000”*.

---

## ✨ **Example Conversation**

**User:**  
> “Plan a 4-day trip to Manali for ₹8000.”

**TripMate.AI:**  
> 🏔 *Here’s your 4-day Manali itinerary!*  
> **Day 1:** Arrival & Mall Road walk  
> **Day 2:** Solang Valley adventures  
> **Day 3:** Hadimba Temple & Old Manali  
> **Day 4:** Departure  
> 💸 Total: ₹7800

---

## 🌌 **Future Enhancements**
- 🌤 Real-time weather integration  
- 🚌 Transport recommendations  
- 🏨 Auto-booking with Google Maps API  
- 💬 Multi-language travel assistant mode

---

## 👩‍💻 **Author**
**Vahini Muttineni**  
Creator of **TravelPlanner** — a WhatsApp-based travel planner using n8n, Gemini AI & Google Sheets.
