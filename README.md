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
- Privacy-first compressed cookie: stores previous entries when "Remember this entry after CREATE" is checked
- Autocomplete on Event Title from stored history (substring filter)
- **Import .ics / .ical** — load an existing calendar file directly into the form (sanity-checked, all fields populated)

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
https://docfingo.github.io/qr/?title=Team+Standup&startDate=2025-10-01&startTime=09:00&endDate=2025-10-01&endTime=09:30&location=Room+3B&description=Weekly+sync&organizer=alice@example.com
```

---

## Privacy

- All processing is local — no data ever leaves your browser
- Cookie for saved entries (not a tracker): `qr_gen_prefs`
- Cookie is only written when "Remember this entry after CREATE" is checked on form submission (compressed via deflate-raw)
- Cookie expiry: 3 years, `SameSite=Strict`
