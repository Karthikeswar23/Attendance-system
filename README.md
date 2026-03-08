# Attendance-system (Anti-Proxy)

A secure, web-based attendance system designed to prevent "proxy" attendance. This system uses multi-layered verification to ensure students are physically present in the classroom and are not marking attendance for others.

## 🚀 Key Features

*   **WiFi Verification (IP Lock):** Automatically compares the Teacher's public IP with the Student's public IP. Attendance is blocked if the student is not on the same network.
*   **Device Fingerprinting:** Uses `FingerprintJS` to generate a unique digital ID for every phone hardware. Prevents a student from marking multiple people using one phone (even in Incognito mode).
*   **QR Code Automation:** Generates a dynamic QR code that auto-fills and locks the Room Code for the student.
*   **Daily Reset Logic:** Automatically allows students and devices to submit again the next day, while blocking duplicates within the same 24-hour window.
*   **Zero-Cost Hosting:** Uses Google Sheets as the database and Google Apps Script as the backend.

## 🛠️ Security Layers

| Security Layer | Technology | Prevents |
| :--- | :--- | :--- |
| **Location Lock** | IP Matching (Ipify API) | Students marking attendance from home/outside. |
| **Hardware Lock** | Browser Fingerprinting | Students marking for friends using Incognito/Private tabs. |
| **Browser Lock** | LocalStorage | Accidental double-submissions. |
| **Identity Lock** | Server-side Validation | Using the same name twice in one day. |

## 📋 Setup Instructions

### 1. Google Sheets Configuration
1. Create a new Google Sheet named `Attendance_Database`.
2. Create two tabs (worksheets) at the bottom:
   *   **Sessions:** Add headers `Room Code`, `Teacher IP`, `Time Created` in the first row.
   *   **Attendance:** Add headers `Date`, `Time`, `Name`, `Batch`, `DeviceID` in the first row.

### 2. Google Apps Script (Backend)
1. In your sheet, go to **Extensions > Apps Script**.
2. Copy the code from `Code.gs` and paste it there.
3. Click the **Gear icon (Settings)** and check "Show 'appsscript.json' manifest file".
4. In `appsscript.json`, set your local timezone (e.g., `Asia/Kolkata`).
5. Click **Deploy > New Deployment**.
   *   **Select Type:** Web App
   *   **Execute As:** Me
   *   **Who has access:** Anyone
6. **Copy the Web App URL** provided.

### 3. Frontend Configuration
1. Open `index.html` (Teacher Dashboard) and `student.html` (Student Page).
2. Locate the variable `const GAS_URL` in both files.
3. Paste your **Web App URL** inside the quotes.
4. Host both HTML files on **GitHub Pages**.

## 🖥️ How to Use

1.  **Teacher:** Open `index.html` on a laptop connected to the classroom Wi-Fi. Click **Take Attendance**. A QR code and Room Code will appear.
2.  **Student:** Scan the QR code using a phone connected to the **same Wi-Fi**.
3.  **Student:** Enter Name and Batch, then click **Submit**.
4.  **Teacher:** View the live entries appearing instantly in your Google Sheet.

## 📂 Project Structure

*   `index.html`: The Teacher Dashboard (QR generation & Session creation).
*   `student.html`: The Student Interface (Fingerprinting & Submission).
*   `Code.gs`: The Google Apps Script logic (Validation & Sheet logging).
*   `README.md`: Project documentation.

## 📜 License
This project is open-source and intended for educational purposes.
