# 📡 Smart Wi-Fi Anti-Proxy Attendance System

A highly secure, serverless classroom attendance system hosted on GitHub Pages and powered by Google Sheets. This system ensures that **only students physically present in the classroom** can mark their attendance, and strictly prevents proxy (fake) attendance using a multi-layered security approach.

## ✨ Features & Security Layers

This system defeats proxy attendance using 4 invisible layers of security:

1. **Same Wi-Fi Enforcement (IP Matching):** 
   The system fetches the Public IP of the teacher's network and compares it with the student's network. If a student tries to submit attendance from their home Wi-Fi or using Mobile Data, the system instantly blocks them.
2. **Device Fingerprinting (Hardware Lock):** 
   When a student submits attendance, the system generates an invisible "Device ID" based on their physical phone screen size and browser data. If a student tries to switch Google accounts or use Incognito Mode to submit a friend's name, the database catches the duplicate Device ID and blocks it. One physical phone = One submission per day.
3. **Active Session Lock:** 
   The backend strictly verifies the Room Code against the *most recently generated* teacher session. Old codes, yesterday's codes, or random guesses are automatically rejected.
4. **Local UI Lock:** 
   Once a student successfully submits their attendance, their browser is locked for the rest of the day. The form becomes invisible, preventing them from easily handing their phone to the person sitting next to them. This lock automatically resets at Midnight.

---

## 🛠️ Tech Stack
* **Frontend:** HTML5, CSS3, Vanilla JavaScript (Hosted on GitHub Pages)
* **Backend:** Google Apps Script
* **Database:** Google Sheets
* **APIs Used:** `ipify` (for fetching Public IP networks), `qrcode.js` (for QR generation)
* **Zero-Cost:** No servers to maintain or pay for.

---

## 🚀 How It Works

### For the Teacher (Host):
1. The teacher connects to the classroom Wi-Fi and opens the Teacher Dashboard.
2. They click **Take Attendance**.
3. The system fetches the classroom router's IP, generates a random 4-digit Room Code, and saves a new active "Session" in Google Sheets.
4. A QR Code and the 4-digit Room Code are displayed on the projector.

### For the Student:
1. Students connect to the **exact same classroom Wi-Fi**.
2. **Mobile users** scan the QR code (which auto-fills the Room Code). **Laptop users** visit the student link and type the code.
3. The student enters their Full Name and Batch Number and clicks Submit.
4. The system verifies their IP address and Device ID. If approved, it saves their attendance with an automatic, tamper-proof Date and Time stamp.

---

## ⚙️ Setup Instructions (For Developers)

If you want to clone this project and set it up for your own classroom, follow these steps:

### Step 1: Set up the Google Sheet (Database)
1. Create a new Google Sheet.
2. Create two tabs (worksheets) at the bottom: 
   * Name the first tab **Sessions**
   * Name the second tab **Attendance**

### Step 2: Set up Google Apps Script (Backend)
1. In your Google Sheet, click `Extensions` > `Apps Script`.
2. Delete any existing code and paste the `Code.gs` script.
3. Click the **Save** icon.
4. Click **Deploy** > **New Deployment**.
5. Choose **Web app**. 
   * Execute as: **Me**
   * Who has access: **Anyone**
6. Click **Deploy**, authorize permissions, and **copy the Web App URL**.

### Step 3: Configure the Frontend
1. Clone this repository.
2. Open `index.html` and `student.html`.
3. Locate the `GAS_URL` constant in both files and replace the placeholder with your copied Google Apps Script Web App URL.
4. In `index.html`, locate the `studentLink` variable and change the URL to match your GitHub Pages hosted repository link.

### Step 4: Host on GitHub Pages
1. Push your files to a public GitHub repository.
2. Go to your repository **Settings** > **Pages**.
3. Under "Build and deployment", set the Branch to `main` (or `master`) and click Save.
4. Your anti-proxy attendance system is now live!

---
*Developed for smart, secure, and hassle-free classroom management.*
