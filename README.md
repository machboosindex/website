# Machboos Index | مؤشر المجبوس

A one-page website that compares supermarket prices in Kuwait and tracks the Machboos Index.
Prices come from a Google Sheet, so updating the site means editing the sheet. No code changes are needed.

## Files

- `index.html`: the whole website. The only part you edit is the `SETTINGS` block near the top of the `<script>`.
- `kuwait-prices-sheet.xlsx`: the price sheet template. Upload it to Google Drive and open it as a Google Sheet.

## One-time setup

### 1. Make the Google Sheet
1. Go to drive.google.com, click **New → File upload**, and upload `kuwait-prices-sheet.xlsx`.
2. Open it, then **File → Save as Google Sheets**. Use this new Google Sheets copy from now on.
3. Click **Share**. Under *General access*, choose **Anyone with the link** as **Viewer**.
4. Copy the sheet's ID from the address bar: the long code between `/d/` and `/edit`.

### 2. Connect the website to the sheet
1. Open `index.html` in a text editor (Notepad on Windows, TextEdit on Mac in plain-text mode, or VS Code).
2. In `SETTINGS`, paste the ID between the quotes: `SHEET_ID: "your-id-here",`
3. Change `SITE_NAME_EN` and `SITE_NAME_AR` to your site's name.
4. Save, then double-click `index.html` to open it in your browser. The green **Updated** label at the top means it's reading your sheet.

### 3. Put it online (free)
1. Create a free account at github.com. Click **New repository**, name it (e.g. `kuwait-prices`), make it **Public**, and create it.
2. On the repository page, click **uploading an existing file**, drag in `index.html` and `README.md`, and click **Commit changes**.
   Don't upload the .xlsx file: the website reads the Google Sheet directly.
3. Create a free account at dash.cloudflare.com. Go to **Workers & Pages → Create → Pages → Connect to Git**, pick your repository, leave the build settings empty, and click **Save and Deploy**.
4. Your site goes live at an address like `kuwait-prices.pages.dev`.

### 4. Add your own domain (optional, about $10.46 a year for a .com)
In Cloudflare, go to **Domain Registration → Register Domains**, buy the name, then open your Pages project → **Custom domains** → add it.

## Every week or month
Add rows to the **prices** tab (month, item, store, price) and one row to the **machboos** tab.
The website shows new prices within a few minutes of a reload. You don't need to re-upload anything.

## Changing the website itself
Edit `index.html`, then upload it to GitHub again (same **Add file → Upload files** button). Cloudflare republishes it automatically within a minute or two.
