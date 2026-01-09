# Dual Timezone Clock

A minimal, professional dual-timezone clock implemented as a single HTML file.

This clock displays one or two selectable time zones with second-boundary synchronization,
and can optionally reference the server clock via HTTP `Date` headers
when hosted on Google Cloud Storage (GCS).

The design philosophy is **maximum clarity with minimum UI**.

---

## Features

- **Dual time zone display**

  - Primary and secondary time zones are freely selectable
  - Secondary display can be shown or hidden

- **Second-boundary synchronization**

  - Updates are aligned to exact second boundaries
  - No cumulative drift from `setInterval(1000)`

- **Server clock reference (optional)**

  - Uses HTTP `Date` header from the hosting server (e.g. GCS)
  - Automatically falls back to the device clock if unavailable
  - Current time source is clearly indicated

- **Keyboard-first interaction**

  - Press `S` to open the settings dialog

- **Persistent settings**

  - Time zones, visibility, and text color are saved in `localStorage`

- **Single-file implementation**
  - HTML, CSS, and JavaScript contained in one file
  - No external dependencies

---

## Time Source Behavior

When hosted on Google Cloud Storage:

- The application periodically sends a `HEAD` request to itself
- The server’s HTTP `Date` header is used as a reference clock
- Network round-trip time (RTT) is compensated (RTT / 2)

If server time is unavailable, the application automatically falls back to the device clock.

Displayed status:

- `time source: server clock`
- `time source: device clock`

---

## Keyboard Shortcuts

| Key | Action               |
| --- | -------------------- |
| `S` | Open settings dialog |

---

## Customization Options

Available via the settings dialog:

- Primary time zone
- Secondary time zone
- Show / hide secondary display
- Text color (curated Material-style colors for readability)

---

## Hosting

This application is designed to work especially well when hosted on:

- **Google Cloud Storage (static hosting)**

However, it also works correctly as:

- A local HTML file
- Any static hosting service

(Server time synchronization may be unavailable depending on the hosting environment.)

---

## Design Philosophy

- No decorative UI elements
- No borders, badges, or unnecessary labels
- Visual hierarchy expressed only through typography and spacing
- Intended for continuous display on a secondary monitor or wall display

---

## Implementation Notes

- Time formatting uses `Intl.DateTimeFormat` with cached formatters
- Time updates are aligned to real second boundaries using adaptive `setTimeout`
- No parsing round-trips through localized strings

---

## About This Project

This application was implemented through an interactive design and engineering process
with **ChatGPT 5.2**, based on explicit functional and aesthetic requirements.

The final structure, behavior, and UX decisions were iteratively refined
to prioritize correctness, clarity, and long-term stability.

---

## License

MIT License
