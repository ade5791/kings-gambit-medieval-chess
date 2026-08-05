# King's Gambit - Medieval 3D Chess (published build)

Live: https://ade5791.github.io/kings-gambit-medieval-chess/

This repository contains **only the gated production build**. It is a publish
target, not the source tree: the bytes here were produced by a single
`vite build`, hashed, gated, and pushed without modification.

## Why the build lives in its own repository

The gate hashes every file in `dist/`, then verifies that GitHub Pages serves
those exact bytes. Mixing source and build output in one branch makes that
contract hard to check and easy to break. `.gitattributes` sets `* -text` and
the repo was committed with `core.autocrlf false`, so git cannot rewrite a
single byte of the gated tree.

`.nojekyll` is present so Pages serves the tree verbatim rather than running it
through Jekyll.

## What was verified before this was pushed

- Typecheck clean, 99/99 unit tests pass.
- 130/130 player-journey QA checks pass against these exact bytes, across
  desktop, touch portrait, touch landscape and reduced-motion surfaces.
- Zero console errors and zero page errors.
- Frame-time distribution sampled on the staged bytes: p50 16.8ms, p95 17.9ms,
  p99 19.2ms.
- Full asset inventory present: 100 files, including 90 model GLBs.

Gate artifacts and the complete measurement record live in the source repo at
`docs/publish/PUBLISH.md`.

## Known limits

Online multiplayer requires a WebSocket relay, which static hosting cannot run.
Hotseat and play-versus-computer are fully functional on this deployment.
