# My Caba – Dr.Althea 345 landing page

Single-page, mobile-first landing page (Arabic / Darija) with a cash-on-delivery order form for 58 wilayas.

Live (GitHub Pages): https://azazmohamed.github.io/mycaba-landing/

## Edit before going live
All settings are in the `CONFIG` block at the bottom of `index.html`:

- `whatsapp`: store number in international format, e.g. `213550000000`. Orders then open as a ready WhatsApp message.
- `sheetUrl`: optional Google Apps Script web-app URL to save each order to a Google Sheet (see below).
- `offers`: titles, prices, quantities, free delivery rules.
- `fees`: example delivery prices per zone (stop desk, home). Replace with your courier's real rates. Each wilaya's zone (A, B, C, D) is in the `WILAYAS` list.

Also replace the placeholders: real jar photo, texture video, batch code / invoice photos, WhatsApp number in the footer, and remove the "نسخة تجريبية" banner and the `noindex` meta tag when you launch.

## Save orders to Google Sheets (optional)
1. Create a Google Sheet, then Extensions → Apps Script, and paste:

```js
function doPost(e) {
  const o = JSON.parse(e.postData.contents);
  const sh = SpreadsheetApp.getActiveSpreadsheet().getSheets()[0];
  if (sh.getLastRow() === 0) sh.appendRow(Object.keys(o));
  sh.appendRow(Object.values(o));
  return ContentService.createTextOutput("ok");
}
```
2. Deploy → New deployment → Web app → Execute as: Me, Who has access: Anyone → copy the URL into `sheetUrl`.
