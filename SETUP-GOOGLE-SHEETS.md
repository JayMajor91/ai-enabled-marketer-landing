# Connect Landing Page → Google Sheets (2 minutes)

## Step 1: Open Apps Script
1. Open your Google Sheet: https://docs.google.com/spreadsheets/d/1BfoGpU-DX5x-9ld9-duXmk4u2bagkET38iLxpFI-xfE
2. Click **Extensions** → **Apps Script**

## Step 2: Paste the Script
1. Delete any existing code in the editor
2. Paste this entire script:

```javascript
const SHEET_NAME = 'Sheet1';

function doPost(e) {
  try {
    const sheet = SpreadsheetApp.getActiveSpreadsheet().getSheetByName(SHEET_NAME);
    if (sheet.getLastRow() === 0) {
      sheet.appendRow(['Timestamp', 'Name', 'Email', 'Role', 'Source']);
    }
    const data = JSON.parse(e.postData.contents);
    sheet.appendRow([
      data.timestamp || new Date().toISOString(),
      data.name || '',
      data.email || '',
      data.role || '',
      data.source || 'landing-page'
    ]);
    return ContentService.createTextOutput(JSON.stringify({ status: 'success' })).setMimeType(ContentService.MimeType.JSON);
  } catch (error) {
    return ContentService.createTextOutput(JSON.stringify({ status: 'error', message: error.toString() })).setMimeType(ContentService.MimeType.JSON);
  }
}

function doGet(e) {
  return ContentService.createTextOutput(JSON.stringify({ status: 'active' })).setMimeType(ContentService.MimeType.JSON);
}
```

3. Click **Save** (💾 icon or Ctrl+S)

## Step 3: Deploy as Web App
1. Click **Deploy** → **New deployment**
2. Click the ⚙️ gear icon → select **Web app**
3. Set:
   - Description: "Lead capture"
   - Execute as: **Me**
   - Who has access: **Anyone**
4. Click **Deploy**
5. Click **Authorize access** → choose your Google account → Allow
6. **Copy the Web App URL** — it looks like: `https://script.google.com/macros/s/XXXXX/exec`

## Step 4: Send me the URL
Paste that URL here in Telegram and I'll update the landing page instantly. Done! ✅
