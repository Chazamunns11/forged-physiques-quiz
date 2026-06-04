# Forged Physiques — "What's Blocking Your Transformation?" Quiz

A single-file, self-contained lead-gen quiz funnel. Black / white / lime (#7DD957) to match the Forged Physiques deck. Mobile-first.

## The file
- **`index.html`** — the finished quiz. This is the only file you upload/host. Everything (logo, transformation photos, fonts trigger, code) is embedded — no broken links, works offline once loaded.
- `quiz_template.html` — build source (has `__TOKEN__` placeholders for the embedded images). Only needed if the images ever change. Ignore it for normal edits.

## How to use it
Upload `index.html` anywhere — GoHighLevel (custom code / page), a static host, or open it locally to demo. That's it.

## The 3 things to swap (top of the file)
Open `index.html`, find the **`CONFIG`** block near the bottom (`<script>` section). Three things to change:

1. **Lead magnet links** — replace each `'#'` with the real download / landing-page URL:
   ```js
   leadMagnets: {
     sleep:      { title: 'The Recovery & Sleep Protocol',    url: '#' },  // ← your link
     habits:     { title: 'The Consistency Blueprint',        url: '#' },  // ← your link
     foundation: { title: 'The Foundation Phase Starter',     url: '#' },  // ← your link
     training:   { title: 'The Training & Execution Playbook', url: '#' }  // ← your link
   }
   ```
   (Titles are editable too if your guides are named differently.)

2. **Booking link** — the soft "book a call" nudge at the end:
   ```js
   bookingUrl: 'https://REPLACE-WITH-YOUR-BOOKING-LINK',
   ```

3. **Lead capture** — currently **capture-only**. Every submission is saved in the browser (`localStorage` key `fp_quiz_leads`) and logged to the console, so you can test immediately. When you're ready to push leads into GHL/Zapier, paste a webhook URL:
   ```js
   leadWebhookUrl: '',   // ← paste your GHL / Zapier / Make webhook here
   ```
   Once set, each lead POSTs as JSON automatically (name, mobile, email, Instagram + their score, blocker and full answers).

## How the result works
- 12 questions, 3 per category: **Sleep & Recovery · Consistency & Habits · Foundation Phase · Training & Execution**.
- Each answer scores 0–3 "health" points. Each category gets a %.
- **Overall "Transformation Readiness %"** = average of the four.
- **#1 blocker** = the lowest-scoring category → that category's lead magnet becomes the headline download. The other three are offered as a "toolkit".

## Testing leads now
Open the page, complete the quiz, then in the browser console:
```js
JSON.parse(localStorage.getItem('fp_quiz_leads'))
```
…to see everything captured.
