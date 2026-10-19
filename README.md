# USEE Message Workspace

Lightweight browser app for managing Outlook campaign messages.

## Features

- Seeding Product and Showcase Link Update templates
- Editable HTML preview
- Copy HTML or plain text
- Save custom templates in the browser
- Product database with PID, commission, and links
- Batch email delivery through a Power Automate HTTP trigger

The product database has two independent catalogs: **Showcase** for link-update
campaigns and **Seeding** for sample-request campaigns. Each catalog is saved
separately in this browser, so editing one cannot overwrite the other.

## Power Automate

Use a **When an HTTP request is received** trigger with this schema:

```json
{
  "type": "object",
  "properties": {
    "EmailList": { "type": "string" },
    "Text1": { "type": "string" }
  }
}
```

The flow should use `Text1` as the HTML **Body** of Outlook's **Send an email (V2)** action. The app sends up to 50 recipients per request and stops when a request returns a non-2xx response.

Keep the Power Automate trigger URL private.

## Hosting

The app is a static site and can be hosted on GitHub Pages. Hosting the UI
publicly does not make the Power Automate flow public or secure it. The browser
must be allowed to call the HTTP trigger from the GitHub Pages origin; if the
flow or tenant blocks browser CORS requests, put an authenticated proxy (for
example an Azure Function or Cloudflare Worker) in front of Power Automate.

For the MVP, the endpoint is only sent when **Send to Outlook** is clicked and
is not saved by the app. Treat the trigger URL like a secret because anyone who
has it can call the flow.
