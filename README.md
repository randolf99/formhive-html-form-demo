[![Releases](https://img.shields.io/github/v/release/randolf99/formhive-html-form-demo?label=Releases&color=2b9348&logo=github)](https://github.com/randolf99/formhive-html-form-demo/releases)

# FormHive HTML Form Demo — Serverless Endpoint, Webhooks, Zapier

![Form backend illustration](https://raw.githubusercontent.com/github/explore/main/topics/html/html.png)

Purpose: show how to collect HTML form submissions without running your own server. You will send form data to formhive.net and use webhooks or Zapier to route the results.

Repository topics: contact-form, form-api, form-backend, form-endpoint, formhive, html-form, no-backend, static-website, webhooks, zapier

Releases: Download the release asset from https://github.com/randolf99/formhive-html-form-demo/releases and execute the included script or archive. The release file contains example HTML, JavaScript, and cURL snippets you can run locally.

Table of contents
- Features
- How it works
- Quick start (HTML)
- JavaScript example (fetch)
- cURL example
- Webhook setup
- Zapier integration
- Files in this repo
- Releases and download
- License

Features
- Receive HTML form submissions without a server.
- Use a hosted form endpoint (formhive.net).
- Forward submissions to webhooks.
- Connect to Zapier for automations.
- Works from static sites, GitHub Pages, and S3-hosted pages.

How it works
- Your HTML form posts to a form endpoint hosted by formhive.net.
- formhive stores and forwards the data.
- You add a webhook URL in the formhive dashboard.
- Webhook receives JSON payloads for each submission.
- Zapier can receive the same payload and trigger workflows.

Design goals
- Minimal setup for static sites.
- Clear fallback for manual HTTP calls.
- Examples for HTML, JavaScript, and cURL.
- Show how to chain a webhook or Zapier trigger.

Quick start — HTML form example
1. Copy the HTML snippet below into your page.
2. Replace FORMHIVE_ENDPOINT with the form endpoint URL you get from formhive.net.
3. Publish the page on any static host.

HTML
```html
<form action="https://formhive.net/api/v1/forms/FORMHIVE_ENDPOINT/submissions" method="post">
  <label>
    Name
    <input name="name" type="text" required>
  </label>
  <label>
    Email
    <input name="email" type="email" required>
  </label>
  <label>
    Message
    <textarea name="message" rows="4"></textarea>
  </label>
  <button type="submit">Send</button>
</form>
```

Notes on fields
- Use standard form field names.
- formhive accepts form-encoded and JSON payloads.
- Add hidden fields for metadata (source, page, campaign).

JavaScript example (fetch)
- Use this sample when you want client-side control.
- This sends JSON to the form endpoint and handles the response.

JavaScript
```js
const endpoint = "https://formhive.net/api/v1/forms/FORMHIVE_ENDPOINT/submissions";

async function submitForm(data) {
  const resp = await fetch(endpoint, {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify(data),
  });

  if (!resp.ok) {
    const text = await resp.text();
    throw new Error(`Submit failed: ${resp.status} ${text}`);
  }
  return resp.json();
}

// Example usage
const formData = { name: "Alice", email: "alice@example.com", message: "Hello" };
submitForm(formData).then(r => console.log("Submitted", r)).catch(e => console.error(e));
```

cURL example
- Use cURL to test the endpoint from the CLI.

cURL
```bash
curl -X POST "https://formhive.net/api/v1/forms/FORMHIVE_ENDPOINT/submissions" \
  -H "Content-Type: application/json" \
  -d '{"name":"Bob","email":"bob@example.com","message":"Test from CLI"}'
```

Webhook setup
- In the formhive dashboard, set a webhook URL where formhive will POST JSON payloads.
- The payload includes:
  - id: submission id
  - form: form id
  - data: key/value object with the submitted fields
  - created_at: ISO timestamp

Example webhook payload
```json
{
  "id": "sub_123456",
  "form": "form_abc",
  "data": {
    "name": "Bob",
    "email": "bob@example.com",
    "message": "Test from CLI"
  },
  "created_at": "2025-08-19T12:34:56Z"
}
```

Security
- Use HTTPS for your webhook receiver.
- Validate incoming requests by checking a signature header if you enable it in the formhive settings.
- Keep sensitive processing on a server you control or use Zapier to handle secrets.

Zapier integration
- Create a Zap that uses a webhook trigger.
- Choose "Catch Hook" or "Catch Raw Hook" depending on your payload needs.
- Copy the Zapier webhook URL into the formhive webhook settings.
- Add Zap actions for email, spreadsheet, Slack, or any Zapier app.

Zap flow example
1. Trigger: Webhooks by Zapier — Catch Hook
2. Action: Google Sheets — Create Spreadsheet Row
3. Action: Gmail — Send Email

Files in this repo
- examples/
  - html-form.html — HTML form demo.
  - js-fetch.js — client-side fetch example.
  - curl-examples.sh — cURL calls for testing.
- docs/
  - webhook-schema.md — JSON schema for webhook payloads.
  - zapier-setup.md — step-by-step Zapier guide.
- LICENSE — repository license.

Releases and download
- Get the packaged examples and scripts from the Releases page.
- Visit and download the release asset at https://github.com/randolf99/formhive-html-form-demo/releases and run the included script or unpack the archive to your local machine.
- The release file bundles all example files and a small shell script to copy examples into a demo folder.

Releases badge
[![Download Release](https://img.shields.io/badge/Download-Releases-blue?logo=github)](https://github.com/randolf99/formhive-html-form-demo/releases)

Common troubleshooting
- 400 Bad Request: check field names and content type (application/json vs form-encoded).
- 401/403: check endpoint token or permission settings in the formhive dashboard.
- No webhook delivery: check your webhook URL for reachable host and valid TLS cert.

Best practices
- Use unique field names per form.
- Add a hidden field for origin to distinguish multiple pages.
- Rate limit downstream processors to avoid spikes.
- Store raw webhook payloads for debugging.

Examples and demos
- Use the HTML file to test basic submit flow.
- Use the JS example to add client-side validation before sending.
- Use cURL to simulate form submissions from scripts or CI.

Contact and support
- Open issues on this repository for code examples and corrections.
- For account or endpoint issues, contact the formhive support channels.

License
- This repo uses the MIT license. See LICENSE for details.