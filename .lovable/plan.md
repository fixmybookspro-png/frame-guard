# Finish the frame-change prefilter in `src/routes/index.tsx`

## Important note on the codebase

This Lovable project currently holds only the blank starter template — the ORACLE code from `fixmybookspro-png/baba-ganoosh` (`oracle-lab`) is not present here, and a GitHub repo can't be pulled into a project from chat. So step 1 below is getting the real file in front of me: either open the Lovable project already synced to that repo (with its branch set to `oracle-lab`) and re-run this request there, or paste/upload the current `src/routes/index.tsx`. Everything after step 1 is the work itself, and it stays scoped to that one file.

## Step 1 — Get the actual `oracle-lab` code

Confirm the existing structure before editing: the camera loop, `grabFrame`, the `/api/coach` call site, the adaptive scan interval logic, the hidden debug panel, and the already-declared `sigRef`, `lastSentAtRef`, `skippedFrames`.

## Step 2 — Compute a frame signature in `grabFrame`

Inside the existing capture path, after the frame is drawn to the offscreen canvas:

- Read pixels once at a tiny scale (e.g. draw/sample down to an 8x8 or 12x12 grid).
- Convert each cell to grayscale (`0.299R + 0.587G + 0.114B`), quantize, and store as a fixed-length numeric array.
- Return the signature alongside the existing frame payload — no change to the image data actually sent.

## Step 3 — Compare against the last sent frame

- Mean absolute difference between the new signature and `sigRef.current`.
- A single tuned threshold constant decides "materially unchanged".
- No previous signature (first frame) always counts as changed.

## Step 4 — Skip rule at the `/api/coach` call site

Skip the request only when all three hold:

1. Frame is materially unchanged versus `sigRef.current`.
2. There is no pending user message.
3. `Date.now() - lastSentAtRef.current` is under ~6000 ms.

On skip: increment `skippedFrames`, leave `sigRef` and `lastSentAtRef` untouched, and continue the loop normally.

User messages always send, regardless of frame similarity or timing.

## Step 5 — Update refs on real sends

When a real `/api/coach` call happens, set `sigRef.current` to that frame's signature and `lastSentAtRef.current = Date.now()`.

## Step 6 — Surface `skippedFrames` in the hidden debug panel

Add one line to the existing panel, matching its current formatting. No new UI, no visual redesign.

## Step 7 — Verify

Run the TypeScript and build checks and fix any errors introduced before stopping.

## Out of scope

No redesign, no stack changes, no new features, no other files touched, and no changes to `main`.
