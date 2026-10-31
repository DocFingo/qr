 # qr — iCal QR Code Generator

**Live:** https://docfingo.github.io/qr/

A fully self-contained, offline-capable HTML5 tool that generates an iCal-formatted QR code for any calendar event. No server, no CDN, no external requests of any kind.

Module data generation is based on [qrcode.min.js](https://github.com/davidshimjs/qrcodejs) (qrcodejs by davidshimjs), inlined into the page and slightly adapted (UTF-8 byte-length handling).

---

## Features

- Generates a valid RFC 5545 iCal `VEVENT` encoded as a QR code
- QR pixel size is always an exact multiple of the QR module grid
- Live QR module size gauge with character progress and remaining headroom indicator
- Remembers your entry history in a private, compressed browser cookie, with title autocomplete
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

All 8 fields are addressable by their ID as query parameters. When any parameter is present, the page auto-generates the QR code and auto-downloads the PNG. If neither `startTime` nor `endTime` is given, the event is created as an all-day event. "Remember this entry" is switched off for that visit (your saved history is not modified).

```
https://docfingo.github.io/qr/?title=Team+Standup&startDate=2025-10-01&startTime=09:00&endDate=2025-10-01&endTime=09:30&location=Room+3B&description=Weekly+sync&organizer=alice@example.com
```

---

## Privacy

- All processing is local — no data ever leaves your browser
- Cookie for saved entries (not a tracker): `qr_gen_prefs`
- Cookie is only written when "Remember this entry after CREATE" is checked on form submission (compressed via deflate-raw)
- Cookie expiry: 3 years, `SameSite=Strict`
