# Sensos Web Proposal

v2 web proposal

## Digital Signature Option

- Overview: Adds an optional digital signature pad under the Pricing section. Users can draw with mouse or touch, clear, save, and export as PNG.
- Data: Saved signature is stored as a base64 PNG in a hidden input (name: signatureData) and shown in a preview.
- No backend: The page does not submit anywhere; use Export to download the PNG locally.

## Email Notifications

This project is static and does not include a backend. To receive emails when users view or sign:

- Provide a webhook URL via the `notify` URL parameter or localStorage.
- The app will POST JSON events to that URL: `view_signature_section`, `cta_review_sign_click`, `cta_fixed_review_sign_click`, `signature_saved`, `signature_downloaded`.

### Quick Setup (Zapier Webhook to Email)

1. Create a Zap: Trigger = “Catch Hook” (Webhooks by Zapier).
2. Copy the webhook URL.
3. Action = “Send Email” to `caseyglarkin2@gmail.com`. Map JSON fields in the email body (event, at, href, userAgent).
4. Open the site with your webhook:

```bash
$BROWSER \
	"http://localhost:8080/?notify=https://hooks.zapier.com/hooks/catch/XXXXXX/YYYYYY"
```

Or set it once:

```js
localStorage.setItem('notify_url', 'https://hooks.zapier.com/hooks/catch/XXXXXX/YYYYYY')
```

Events will start posting automatically on view and clicks.

### How to Use

- Open the page locally and scroll to "Authorize The Proposal".
- Toggle "Add Digital Signature" to enable the canvas.
- Draw your signature, then click "Save" to capture it.
- Click "Export PNG" to download the signature image.
- Use "Clear" to reset the pad.

### Run Locally

Open index.html directly in a browser, or:

```bash
$BROWSER /workspaces/sensos-web-proposal/index.html
```

Or start a quick static server:

```bash
python3 -m http.server 8080 --directory /workspaces/sensos-web-proposal
$BROWSER http://localhost:8080/
```
