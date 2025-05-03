## Features

- Handles incoming appointment requests via Vapi voice calls
- Checks for overlapping appointments before booking
- Logs all appointments to a Google Sheet
- Sends confirmation emails to users after successful booking

## Setup

### 1. Prerequisites

- Python 3.8+
- A Google Cloud service account with Sheets API enabled (`creds.json`)
- A Gmail account with [App Passwords](https://support.google.com/accounts/answer/185833)
- A Google Sheet shared with your service account email

### 2. Environment Variables

Create a `.env` file in your project root:

GOOGLE_APP_MAIL=your-email@gmail.com
GOOGLE_APP_KEY="your-app-password-with-spaces"
GOOGLE_SHEET_ID=your-google-sheet-id

### 3. Install Dependencies

pip install -r requirements.txt

### 4. Google Sheet Setup

- Create a sheet with a tab named `Sheet1`

### 5. Run the App

uvicorn main:app --host 0.0.0.0 --port 8000

### 6. Expose Your API

Use [ngrok](https://ngrok.com/) or similar to get a public URL for Vapi integration:

ngrok http 8000

### 7. Configure Vapi

- Set up your Vapi agent to use your public endpoints:
  - `/checkappointmenttime`
  - `/makeappoint`
- Use the same parameter names as in the FastAPI code.

## API Endpoints

- `POST /checkappointmenttime`: Checks if a time slot is available
- `POST /makeappoint`: Books an appointment, logs to Google Sheets, and sends confirmation email

## How it Works

1. User calls the receptionist via Vapi.
2. The agent collects appointment details and checks slot availability.
3. If available, the appointment is booked, logged, and a confirmation email is sent.
4. All data is stored in your Google Sheet.

---
