# USEE Message Workspace

Lightweight browser app for managing Outlook campaign messages.

## Features

- Seeding Product and Showcase Link Update templates
- Editable HTML preview
- Copy HTML or plain text
- Save custom templates in the browser
- Product database with PID, commission, and links
- Batch email delivery through a Power Automate HTTP trigger

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
