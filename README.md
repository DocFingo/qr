# qr — iCal QR Code Generator

**Live:** https://docfingo.github.io/qr/

A fully self-contained, offline-capable HTML5 tool that generates an iCal-formatted QR code for any calendar event. No server, no CDN, no external requests of any kind.

---

## Features

- Generates a valid RFC 5545 iCal `VEVENT` encoded as a QR code
- QR pixel size is always an exact multiple of the QR module grid
- Dark theme UI
- Download as PNG
- Optional colour inversion (white modules on dark background)
- Privacy-first compressed cookie: stores previous entries when "Remember this entry after CREATE" is checked
- Autocomplete on Event Title from stored history (substring filter)
- "Clear" button resets the form without touching the cookie
- "Forget" button removes a cookie-loaded entry from history

---

## Fields

| Field | Required | iCal property |
|---|---|---|
| Event Title | ✅ | `SUMMARY` |
| Start Date | ✅ | `DTSTART` |
| Start Time | ✅ | `DTSTART` |
| End Date | ✅ | `DTEND` |
| End Time | ✅ | `DTEND` |
| Location | optional | `LOCATION` |
| Description | optional | `DESCRIPTION` |
| URL | optional | `URL` |
| Organizer / Contact | optional | `ORGANIZER` |

---

## URL Parameters

All 9 fields are addressable by their ID as query parameters. When any parameter is present, the page auto-generates the QR code and auto-downloads the PNG.

```
https://docfingo.github.io/qr/?title=Team+Standup&startDate=2025-10-01&startTime=09:00&endDate=2025-10-01&endTime=09:30
```

| Parameter | Example |
|---|---|
| `title` | `My+Event` |
| `startDate` | `2025-10-01` |
| `startTime` | `09:00` |
| `endDate` | `2025-10-01` |
| `endTime` | `10:00` |
| `location` | `Room+3B` |
| `description` | `Weekly+sync` |
| `url` | `https://meet.example.com` |
| `organizer` | `alice@example.com` |

---

## Privacy

- All processing is local — no data ever leaves your browser
- Cookie name: `qr_gen_prefs`
- Cookie is only written when "Remember this entry after CREATE" is checked on form submission (compressed via deflate-raw)
- Cookie expiry: 3 years, `SameSite=Strict`
- The "Invert colours" checkbox is never saved to the cookie
