# Forged Physiques — "What's Blocking Your Transformation?" Quiz

A single-file, self-contained lead-gen quiz funnel. Black / white / lime (#7DD957) to match the Forged Physiques deck. Mobile-first.

**It does this:** 15 questions → personalised "Transformation Readiness" score → the client's **#1 blocker** → the matched lead magnet to grab → their **full report emailed** to them → **book-a-call** CTA to remove every blocker.

## The file
- **`index.html`** — the finished quiz. The only file you upload/host. Logo, transformation photos and code are all embedded — no broken links.
- `quiz_template.html` — build source (has `__TOKEN__` placeholders for the embedded images). Only needed if the images change. Ignore for normal edits.

## How to use it
Upload `index.html` anywhere — GoHighLevel (custom code / page), a static host, or open it locally to demo.

## What to swap (the `CONFIG` block, top of the `<script>`)

### 1. Lead magnets — replace each `'#'` with the real link
One bucket per PDF. `cta` = button verb, `kicker` = small label.
```js
leadMagnets: {
  sleep:      { title: 'The Sleep Lead Magnet',     url: '#', cta: 'Download', kicker: 'Free Guide'   },
  morning:    { title: 'The Morning Routine Guide', url: '#', cta: 'Download', kicker: 'Free Guide'   },
  habits:     { title: 'The Habit & Routine Guide', url: '#', cta: 'Download', kicker: 'Free Guide'   },
  foundation: { title: 'The Foundation Phase PDF',  url: '#', cta: 'Download', kicker: 'Free Guide'   },
  training:   { title: 'The Training Webinar',      url: '#', cta: 'Watch',    kicker: 'Free Webinar' }
}
```
Titles are editable — rename to match your real PDFs/webinar.

### 2. Booking link
```js
bookingUrl: 'https://REPLACE-WITH-YOUR-BOOKING-LINK',
```

### 3. Email the personalised report — pick ONE option

**Option A — GoHighLevel / Zapier (recommended for your stack).** Paste your webhook:
```js
leadWebhookUrl: 'https://your-ghl-or-zapier-webhook',
```
Every submission POSTs the full result as JSON. Build a GHL/Zapier workflow that emails the client using these fields:

| Field | Example |
|---|---|
| `firstName`, `lastName`, `email`, `mobile`, `instagram` | contact details |
| `readinessScore` | `62` |
| `verdict` | `So Close` |
| `primaryBlocker` / `blockerLabel` | `sleep` / `Sleep` |
| `blockerDescription` | the diagnostic paragraph |
| `matchedResource.title` / `.url` / `.cta` | the lead magnet to send them |
| `categoryScores` | `{sleep, morning, habits, foundation, training}` |
| `answers` | every question + their choice |

**Option B — EmailJS (no CRM needed, sends straight from the page).** Free at [emailjs.com](https://www.emailjs.com): create a service + an email template, then paste your keys:
```js
emailjs: { publicKey: 'xxx', serviceId: 'service_xxx', templateId: 'template_xxx' },
```
In your EmailJS template, set **To = `{{email}}`** and use merge fields:
`{{first_name}}`, `{{readiness_score}}`, `{{verdict}}`, `{{blocker}}`, `{{blocker_description}}`, `{{resource_title}}`, `{{resource_url}}`, `{{score_sleep}}`, `{{score_morning}}`, `{{score_habits}}`, `{{score_foundation}}`, `{{score_training}}`, `{{booking_url}}`.

> Until A or B is configured, leads are still captured (browser `localStorage` + console) so you can test — the on-page "we've emailed your report" line only appears once an email method is live.

## How the score works
- **5 buckets, 3 questions each (15 total):** Sleep · Morning Routine · Habits & Routine · Foundation Phase · Training.
- Each answer scores 0–3. Each bucket → a %.
- **Transformation Readiness %** = average of the five.
- **#1 blocker** = the lowest-scoring bucket → its lead magnet becomes the headline CTA; the other four are offered as a toolkit.

## Test it now
Complete the quiz, then in the browser console:
```js
JSON.parse(localStorage.getItem('fp_quiz_leads'))
```
…to see the full captured result.
