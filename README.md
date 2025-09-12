# Testmail Viewer

Single-file (single-page) HTML utility for quickly viewing emails via the **Testmail JSON API** without any backend.

## Purpose
This tool lets you locally inspect test inbox messages: list emails, select one, and display its HTML body inside an iframe. There is no server component—just a static file you can open directly or host on GitHub Pages.

## Features
- Manual input of `API Key`, `namespace`, optional `tag`, and result `limit`
- Persists values in `localStorage` so you don't re-enter them each time
- `Refresh` button to fetch the current messages
- Email list with subject, sender, tag, and timestamp
- HTML body rendering of the selected email
- `Clear` button to wipe saved configuration

## What is stored locally
All entered values (`API Key`, `namespace`, `tag`, `limit`) are stored in the browser's `localStorage` under the key `testmailViewerConfigV1`.

Nothing else is sent anywhere except a direct request to the Testmail API. Removing the item from `localStorage` (via the `Clear` button or manually) erases it. The API key is **not** embedded in the file—you supply it at runtime.

## Outgoing request
Exactly one HTTP GET request is made to the public endpoint:

```
https://api.testmail.app/api/json?apikey=...&namespace=...&tag=...&limit=...
```

Parameters:
- `apikey` – your key (taken from the input field)
- `namespace` – your namespace
- `tag` (optional) – exact tag filter
- `limit` – number of emails (1–100)

The response (simplified) includes an `emails` array; each entry may contain `id`, `subject`, `from`, `tag`, `timestamp`, `html`, etc. The `html` field is injected into an iframe for display.

## Usage
1. Open `testmail-viewer.html` locally (double click or drag into your browser). Optionally host it on GitHub Pages.
2. Enter your `API Key` and `namespace` (required).
3. (Optional) enter a `tag` and adjust `limit`.
4. Click `Refresh` to load messages.
5. Click an email on the left to view its HTML on the right.
6. Use `Clear` to remove persisted values.

If an email has no HTML body, a placeholder message is shown instead.

## Security Notes
- API key lives only in your browser's `localStorage`.

