# PyQuest

A browser-based, gamified Python foundations experience for absolute beginners. Three zones, written as a fairy-tale arc — the Awakening Grove (`print`, variables), the Skeleton King's Keep (`for` loops), and the Function Foundry (`def`) — wrap real Python in fiction so non-programmers write working code without ever feeling like they're studying.

The full thirty-to-forty-five-minute run takes a player from a pulsing rune in a dark room to a final showdown with the Null Dragon, casting real Python at every step. Pyodide runs CPython in the browser; nothing is simulated.

## Play it live

**[https://florianmuljono.github.io/pyquest/](https://florianmuljono.github.io/pyquest/)**

Hosted on GitHub Pages. Open the URL in a modern desktop browser (Chrome recommended) — first load takes a few seconds while Pyodide boots, then the rune appears.

## Run it locally

No build, no install, no dependencies. Clone the repo and open `index.html` in a browser, or serve the directory with any static file server (e.g. `python3 -m http.server`).

## Tech stack

- HTML, CSS, vanilla JavaScript — no framework, no build step
- [Pyodide](https://pyodide.org) via CDN for in-browser Python execution
- [CodeMirror 6](https://codemirror.net) via CDN for the code editor (later phases)
- LocalStorage for save state
- GitHub Pages for hosting

## Project documents

- [CLAUDE.md](./CLAUDE.md) — working brief
- [pyquest-build-plan.md](./pyquest-build-plan.md) — strategy
- [pyquest-game-systems.md](./pyquest-game-systems.md) — encounter and boss design
- [pyquest-content.md](./pyquest-content.md) — all hand-written in-game text

## License

Released under the [MIT License](./LICENSE). Free to use, modify, and distribute with attribution.

Built for the Claude hackathon.
