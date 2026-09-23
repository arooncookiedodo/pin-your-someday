# Pin Your Someday

**Pin today's dreams. Meet them again someday.**

Live: https://pin-your-someday.vercel.app

A digital treasure map (vision board) inspired by Toshitaka Mochizuki's book on treasure maps (Korean edition: 《당신의 소중한 꿈을 이루는 보물지도》). Turn each dream into a card, pin it to a board for today or this month, keep versions in an archive with a note to your future self, and publish any board as a standalone HTML file. It's a single HTML file with no install, no account and no server. Everything stays in your browser.

Built in one session with Claude Code and Claude Opus 5.5 for the Seoul | Claude Fable 5.1 Build Day (2026-09-23).

## Run

Double-click `index.html` to open it in Chrome or Edge.

Or serve it locally:

```
python -m http.server 8000
```

Then open http://localhost:8000.

## Use

Everything on a board is a **dream card** with the same fields as the Dreams library: photo (optional), title, description, category, and target month (or "Someday").

- **Board | Dreams | About**: the tabs in the header switch between the board, the Dreams library, and the About intro (Korean). The About view opens automatically on the very first visit; after that the app starts on the board. `#dreams` / `#about` in the address open those views directly.
- **Board title**: the board title is shown large on the board (serif headline with an orange underline). Double-click to edit it in place (Enter saves, Esc cancels), drag to move, drag the round handle to change its size. The ⋯ menu hides or shows it. It is decoration only, so it is not part of Dreams or the archive comparison.
- **Date**: pick a date in the header. Each date has its own board. On a new date you can start blank or click "Start from the … board" to copy the most recent one. "Saved boards" jumps to any saved date.
- **Rename**: click the title (each board has its own title)
- **+ Dream**: opens the dream card form and pins the card to the board. "Also keep in Dreams" (on by default, remembered) saves a copy to the library too.
- **Photos**: drop one photo on the board or paste one with Ctrl+V / ⌘V to open the form with that photo. Dropping several photos pins them straight away as untitled cards.
- **Edit**: double-click a card, press Enter, or use "Edit" in the selection toolbar. The same form is used everywhere.
- **Move**: drag. **Resize**: drag the round handle at the bottom right (photo cards keep their shape; hold Shift to stretch)
- **Selection toolbar**: Edit, Save to Dreams, Bring to front, Send to back, Delete. Delete/Backspace also deletes (ignored while typing).
- **Dreams library**: card grid with search, category filters, and sorting (target date, newest, A–Z). Click a card to edit or delete it. "Add to board" **copies** the dream onto the current date's board and switches back to it. Editing or deleting a dream never changes cards already on boards. "✓ on this board" marks dreams copied onto the current board.
- **Keep ▾ → Save to archive…**: keeps the current board as a version you can look back on years later, with an optional note to your future self. Nothing is archived automatically.
- **Archive**: opens a panel listing kept versions by year and month. Each shows which dreams (by title) appeared or disappeared since the previous version. **View** opens it as HTML in a new tab, **Download** saves that HTML file, and **Delete** removes it.
- **⋯ menu**: "About My Treasure Map" opens the About view (`about.html` is kept as a standalone copy). "Clear this board" removes the current date's board. "Delete all boards…" wipes every saved board after you type `RESET`. Neither can be undone; Dreams, the archive and published HTML files are kept.
- **Keep ▾ → Publish as HTML**: downloads `my-treasure-map-YYYY-MM-DD.html`, a read-only copy of the board with the photos embedded. It shows the title, the board date, and "Published <date & time>"; the publish time is also stored in `<meta name="published-at">`.

## Language

The **EN | 한국어** switch in the top-right corner of the header changes the whole app: buttons, menus, forms, messages, dates ("By Jun 2027" / "2027년 6월까지"), built-in category names, the About view, and the wording of published HTML files. The first visit follows the browser language (Korean if the browser is set to Korean, otherwise English), and the choice is remembered. Text you write yourself (dream titles, board titles, notes) is never translated. Categories are stored under their English names, so filters and colours stay the same in both languages.

## Design

Theme "Paper gallery" uses the Claude core palette (ivory, dark, orange, blue, green). Cards get a small automatic tilt that stays fixed per card. The tape (and a text card's paper) takes the category colour.

## Storage

Boards autosave to IndexedDB (database `treasure-map-boards`: `boards` holds one record per date, plus `dreams`, `snapshots` (archive), and `images`, which stores each photo once for Dreams and the archive). Photos are downscaled to 1200px JPEG. Dreams also keep a small thumbnail for the grid.

- Saved data is separate for each browser and each address (`file://` vs `localhost`).
- Clearing site data in the browser deletes your boards. Published HTML files work as backups for viewing.
- A board saved by the older localStorage version is moved to today's date on first load. The original data is left in localStorage.
- Boards made before dream cards (plain images and notes) are converted when opened: images become photo cards, and a note's first line becomes the title with the rest as the description.

`about.html` is a standalone Korean copy of the About content that uses the English button names. The in-app About tab is the up-to-date, bilingual version.
