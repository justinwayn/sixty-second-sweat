# 60-SECOND SWEAT

**One button. One minute. One blob.**

Press the giant GO button. A cheerful blob coach does a random 60-second bodyweight move *with* you. Finish the minute and your day streak grows. That's the whole app.

Built Oct 28, 2026 — Dillon Ventures. Worldwide Hunt candidate #2 (28/30 on Justin's six tests · Billionaire Algorithm 78 GO, highest of the field). Its job in the fleet: **GodBod's free front door.** People meet the blob here; the ones who want a real trainer walk through the door on the finish screen into GodBod.

**Live:** https://justinwayn.github.io/sixty-second-sweat/
**GodBod door (finish screen):** https://justinwayn.github.io/godbod-test-kit/ — the verified tester-kit page (built & verified Oct 20, 2026, memory 2026-10-20; Lead Runner re-verified PASS Oct 28). GodBod itself is IN REVIEW at Google — nothing in this app claims it is live in any store, and nothing may be edited to claim that until the Play listing is destination-verified.

---

## THE DESIGN LAW — READ BEFORE EDITING

**Sweat stays deliberately dumb.** This is not a limitation; it is the product.

- ONE button. One minute. One move. One blob.
- **No plans, no tracking, no accounts, no settings, no library, no jargon.**
- The only data kept is the streak (localStorage, on the phone, nowhere else).
- If a feature idea smells like GodBod — programs, logs, history, choices — it does **not** belong here. It belongs behind the finish-screen door, in GodBod. Sweat feeds GodBod; it never competes with it.
- The blob's moves are shown, not explained. Labels are 3 words or less. Numbers and the blob carry the app across every language on Earth.

Any future editor who "improves" this into a small GodBod has broken the one rule that makes it work. If it's complicated, it's trash.

---

## How it works

Single file: `index.html` (HTML + CSS + JS, no build step, no dependencies besides the Baloo 2 webfont).

- **Flow:** Home → tap GO → 3-2-1 countdown → 60-second move (big countdown number + shrinking progress bar + the blob animating the move) → finish screen (confetti, streak, GodBod door) — or tap ✕ mid-minute → "The blob believes in you" screen, no shame, no streak penalty.
- **The blob** is one inline-SVG character (body, two arms, two feet, face) animated procedurally with CSS keyframes — each move is a `data-move` attribute on the stage that switches the animation set. Blinking, breathing, and a celebration hop included.
- **Timer** is timestamp-based (`endTime - Date.now()`), so a throttled/backgrounded tab still finishes on time; a Wake Lock is requested during the minute where the browser allows it.
- **Streak** (`localStorage`): `sss_streak` (consecutive days), `sss_lastDay`, `sss_total`. Completing a minute today after one yesterday grows the streak; a missed day restarts it at 1; extra minutes the same day don't double-count.
- **Sounds** are tiny WebAudio beeps (countdown, start, finish arpeggio). No audio files.

## The move pool (14)

March in Place · Wall Push-Ups · Sit to Stand · Arm Circles · Side Steps · Chair Squats · Knee Lifts · Calf Raises · Heel Taps · Shoulder Rolls · Shadow Boxing · Star Arms · Side Reaches · Balance Wobble (switches legs at the 30-second mark)

All bodyweight, joint-friendly, no equipment except a chair and a wall for the two moves named for them. A move never repeats back-to-back.

## Run / deploy

- **Local:** open `index.html` in any browser, or `python3 -m http.server` in this folder.
- **Deploy (fleet pattern, $0):** this folder is the repo `justinwayn/sixty-second-sweat`; GitHub Pages serves `main` at the live URL above — the same pattern as the GodBod tester kit. To republish: commit and `git push`. Pages rebuilds in about a minute; verify the URL returns 200 and the served bytes match the repo file before calling it live anywhere.
- No accounts, no spend, no backend. Render is not used (fleet hosts are GitHub Pages / Vercel; Render stays suspended until Nov 1).

## Verification record (Oct 28, 2026)

Automated end-to-end run (jsdom, real page, real clicks, timer fast-forwarded): **24/24 checks passed** — boot, countdown hand-off, move display, 60s completion, streak 0→1, same-day re-finish does not double-count, early-quit path shows the encouragement screen and leaves the streak untouched, next-day finish grows the streak 1→2, GodBod door present with the verified tester-kit URL.

**Impeccable gate** (detector, static scan of `index.html`): exit 0 — all `low-contrast` findings fixed (deepened text oranges/greens to AA, removed opacity-blended sub-label). One advisory accepted with reason: `shape-assembled-illustration` — the blob is a procedurally animated character rig drawn to the approved concept art (`concept-art.webp`, from the Worldwide Hunt); primitive-shape construction is how it moves. Detector scans are static; no rendered-browser pass was possible on this VM.

## Files

- `index.html` — the whole app
- `concept-art.webp` — the approved concept visual (blob, sky, giant number, GO button) the UI was styled from
- `README.md` — this file
