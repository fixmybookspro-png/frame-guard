# Frame Guard

Use this existing GitHub repository as the codebase for this project:

https://github.com/fixmybookspro-png/baba-ganoosh.git

Do NOT create a new app from scratch.

Work from the existing repository and existing architecture.

Use the oracle-lab branch, not main.

First inspect the current code and continue the partially completed frame-change prefilter in src/routes/index.tsx.

Do not redesign anything. Do not replace the stack. Do not add unrelated features.

The current unfinished work already includes:

sigRef

lastSentAtRef

skippedFrames

Finish only this:

compute a small grayscale frame signature in grabFrame

compare against the previous sent frame

skip /api/coach when the frame is materially unchanged, there is no user message, and the last real AI send was under about 6 seconds ago

always send user messages

update the previous signature and last sent timestamp when a real call occurs

show skippedFrames in the existing hidden debug panel

preserve adaptive scanning and all existing ORACLE behavior

run the TypeScript/build checks and fix errors before stopping

Do not modify main.

This project was built with [Lovable](https://lovable.dev).

## Build with Lovable

Continue developing this project in the [Lovable editor](https://lovable.dev/projects/0493de0a-30fa-4a3b-a676-dfd57fbaeb51).

- **Ship faster**: describe what you want to build and Lovable handles the code.
- **Stay in sync**: every change made in Lovable is committed straight to this repository.
- **Full ownership**: this code is yours. Push to `main` on GitHub and your changes sync back into Lovable, ready for your next prompt.

## Development

Prefer working locally? You need Node.js and npm — [install with nvm](https://github.com/nvm-sh/nvm#installing-and-updating).

```sh
git clone <this-repository-url>
cd <repository-name>
npm i
npm run dev
```
