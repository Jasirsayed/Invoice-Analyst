# Ledgerly — Invoice Intelligence

Upload daily, weekly, and monthly invoices (scanned images or PDFs). Ledgerly reads each
one, extracts the **vendor, dates, due date, currency and total**, and builds an
**Excel + PDF report with charts and analytics**.

Everything runs **100% in the browser** — no server, no sign-up, no upload. Your invoices
never leave your device. Perfect for free static hosting on **GitHub Pages**.

## Features

- **Smart extraction** — editable PDFs are read directly via `pdf.js` (near-perfect accuracy);
  scanned PDFs and images fall back to `Tesseract.js` OCR automatically.
- **Currency- and locale-aware parsing** — handles `$ € £ ₹ ¥`, `1,234.56` and `1.234,56`,
  plus DMY / MDY date order.
- **Editable table** — every field is correctable inline; totals and charts update live.
- **Analytics dashboard** — value over time, spend by period type, top vendors, and an
  overdue-vs-upcoming due-date view.
- **One-click reports** — `.xlsx` (data + summary sheets) and `.pdf` (KPIs + embedded charts + table).
- **Persistent** — data is saved locally in your browser (IndexedDB) and survives refresh.

## Run locally

It’s a single file — just open `index.html` in a browser. (Internet is needed once so the
browser can fetch the open-source libraries from their CDNs.)

For OCR to behave best, serve it over a local web server instead of `file://`:

```bash
python3 -m http.server 8000
# then open http://localhost:8000
```

## Host on GitHub Pages (free)

1. Create a new GitHub repository (e.g. `ledgerly`).
1. Add **`index.html`** (and optionally this `README.md`) to the repo and push.
1. In the repo: **Settings → Pages → Build and deployment**.
1. Set **Source = Deploy from a branch**, **Branch = `main`**, folder = **`/ (root)`**, then **Save**.
1. Wait ~1 minute. Your app is live at `https://<your-username>.github.io/<repo>/`.

That’s it — no build step, no framework, no backend.

## How extraction works

|Input           |Path                                                  |
|----------------|------------------------------------------------------|
|Editable PDF    |`pdf.js` pulls the embedded text layer (most accurate)|
|Scanned PDF     |rendered to canvas → `Tesseract.js` OCR               |
|Image (PNG/JPG…)|`Tesseract.js` OCR                                    |

Each record gets a **confidence score**. OCR on real-world layouts is imperfect, so the
table is fully editable — fix anything that looks off and the report updates instantly.
Field detection keys off common invoice labels (*Total Due*, *Amount Payable*, *Invoice Date*,
*Due Date*, *Invoice No.*, etc.).

## Libraries (all open-source, loaded via CDN)

pdf.js · Tesseract.js · SheetJS (xlsx) · jsPDF + autotable · Chart.js

## Privacy

No analytics, no tracking, no network calls with your data. Files are processed in memory
and stored only in your own browser. Use **Clear all** to wipe everything.

## License

MIT — do whatever you like.