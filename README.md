# Baby Name Finder (QVAC)

Search names by **what they mean**. Type a meaning you love, like "light", "brave", "the sea" or "peace", and find names from many cultures whose meanings are closest, from a list of 83. Filter by girl, boy or unisex and by first letter, build a **shortlist**, rate names with stars, and see how each one sounds with your last name.

It runs **on your own computer** using [QVAC](https://github.com/tetherto/qvac), Tether's open-source AI SDK.
No API key, no cloud service, and what you type never leaves your machine.

![screenshot](screenshot.png)

## SDK version

`@qvac/sdk` **0.19.0** (declared in `package.json`)

Functions used: `loadModel` and `embed`, with the `EMBEDDINGGEMMA_300M_Q4_0` model.

## Install

You need [Node.js](https://nodejs.org) 22 or newer and some free disk space for the model.

```bash
git clone https://github.com/misaki-codex/qvac-baby-name-finder.git
cd qvac-baby-name-finder
npm install
```

## Run

```bash
npm start
```

Then open **http://localhost:3080** (the address, not the HTML file). The first start downloads the model.
While it loads, names are matched by exact words in their meanings instead.

## How it works

- `names.js` holds 83 names with their most common meaning and origin. Add your own.
- `server.js` applies the filters, then compares your words with each name's meaning using QVAC's `embed` and returns the 8 closest.
- Name meanings can differ between sources and cultures, so the app says so. Your shortlist is saved in your browser.
- The server listens on `127.0.0.1`, so only your own computer can reach it.

## Troubleshooting

If you see `RPC_INIT_TIMEOUT`, the QVAC worker was slow to start. `server.js` already waits 3 minutes.
Set `QVAC_RPC_INIT_TIMEOUT_MS` (milliseconds) before `npm start` to wait longer, and make sure no other
QVAC app is running at the same time. If you see `ERR_MODULE_NOT_FOUND`, delete the `node_modules` folder
and run `npm install` again (this usually means an install was interrupted, for example by a full disk).

## License

MIT
