# Email Brain

A "second brain" style marketing visual: an inbox rendered as a living, glowing
graph. Emails are nodes clustered around category hubs, with extra links between
emails from the same sender. Interactive — click a node and its connections
light up.

No frameworks, no build step, no dependencies. Just static HTML/CSS/JS.
Rendered with **SVG** (vectors) so mobile zoom stays sharp.

![Email Brain](preview.png)

## Interactions

- **Click a node** — its connections light up, everything else dims, and a
  detail card shows the email and its links (click a link to jump to that node).
- **Hover** — preview a node's connections.
- **Drag a node** — pull it around; the physics settles it back.
- **Scroll / pinch** — zoom (zooming in reveals sender labels).
- **Drag the background** — pan.

## Run it

Either open `index.html` directly in a browser, or serve it:

```bash
python3 -m http.server 8899
# then open http://localhost:8899
```

Any static host works too (GitHub Pages, Vercel, Netlify, S3).

## Use your own data

Everything is driven by **`data.js`** — one object, `window.EMAIL_BRAIN`, with
`categories` and `emails`. Replace it with a real inbox and the graph rebuilds
itself.

For local overrides without editing the committed demo file, add **`data.local.js`**
(same format as `data.js`, gitignored). It loads after `data.js` and replaces
`window.EMAIL_BRAIN`.

**Do not commit real mailbox data.** Subjects, senders, and snippets can contain
PII. Keep production inbox exports in `data.local.js` or regenerate `data.js` only
when you intend to publish sanitized data.

**See [`DATA_GUIDE.md`](DATA_GUIDE.md)** for the full schema, categorization
heuristics, sizing tips, and how to convert a raw mailbox into `data.js`.

## Files

| File               | Purpose                                                        |
| ------------------ | ------------------------------------------------------------- |
| `index.html`       | Page shell + overlay UI (header, legend, detail card).        |
| `styles.css`       | Styling for the dark "neural" look.                           |
| `data.js`          | **Demo data.** Safe to commit; replace for your own inbox.    |
| `data.local.js`    | Optional local override (gitignored). Loads after `data.js`.  |
| `viewport-guard.js`| Counter-transform for Safari page pinch-zoom on mobile.       |
| `graph.js`         | Force simulation + SVG rendering + interactions.              |
| `DATA_GUIDE.md`    | How to organize email data to build this UI.                  |

**Mobile Safari:** pinch-zoom is handled in-app. If page zoom still slips through,
add `?debug=1` to show a small viewport diagnostic chip.

## License

MIT
