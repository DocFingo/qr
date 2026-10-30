 # qr — iCal QR Code Generator

**Live:** https://docfingo.github.io/qr/

A fully self-contained, offline-capable HTML5 tool that generates an iCal-formatted QR code for any calendar event. No server, no CDN, no external requests of any kind.

---

## Features

- Generates a valid RFC 5545 iCal `VEVENT` encoded as a QR code
- QR pixel size is always an exact multiple of the QR module grid
- Live QR module size gauge with character progress and remaining headroom indicator
- Dark theme UI
- Download as PNG
- Optional colour inversion (white modules on dark background)
- Privacy-first compressed cookie: stores previous entries when "Remember this entry after CREATE" is checked
- Autocomplete on Event Title from stored history (substring filter)
- **Import .ics / .ical** — load an existing calendar file directly into the form (sanity-checked, all fields populated)
- "Clear form" button resets the form without touching the cookie
- Red × in the autocomplete list removes a stored entry from history

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
| Organizer / Contact | optional | `ORGANIZER` |

---

## URL Parameters

All 8 fields are addressable by their ID as query parameters. When any parameter is present, the page auto-generates the QR code and auto-downloads the PNG.

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
| `organizer` | `alice@example.com` |

---

## Buttons

| Button | Action |
|---|---|
| **CREATE QR CODE** | Validates the form and generates the QR code |
| **Import .ics** | Opens a file picker (`.ics` / `.ical`), parses the first VEVENT and fills all form fields |
| **Clear form** | Resets the form; cookie history is not affected |

---

## Privacy

- All processing is local — no data ever leaves your browser
- Cookie name: `qr_gen_prefs`
- Cookie is only written when "Remember this entry after CREATE" is checked on form submission (compressed via deflate-raw)
- Cookie expiry: 3 years, `SameSite=Strict`
- The "Invert colours" checkbox is never saved to the cookie
