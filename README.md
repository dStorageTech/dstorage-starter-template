# dStorage Starter Template

A minimal Node.js/TypeScript project, plus a small Vite browser app, for following the
[dStorage SDK guides](https://dstorage.pro/docs/guide/). Clone it and run it, then swap in each
guide's adapters as you work through the series. You can also use it as boilerplate for your
own app.

## Prerequisites

- Node.js 22 or later
- npm

## Quick start

```bash
git clone https://github.com/dStorageTech/dstorage-starter-template.git
cd dstorage-starter-template
npm install
npm start
```

Out of the box, `npm start` runs the code from the
[Mock Adapters](https://dstorage.pro/docs/guide/mock-adapters.html) guide. It configures the SDK with
in-memory adapters, stores an encrypted string, retrieves and decrypts it, and prints the result.
No external services are needed.

## Project layout

| Path                            | Purpose                                                                 |
| ------------------------------- | ----------------------------------------------------------------------- |
| `src/index.ts`                  | Node.js entry point (`npm start`): Mock, Local & Simulator, and Managed Payments guides |
| `index.html`, `src/main.ts`     | Browser entry point (`npm run dev`): Midnight Network Adapter and Passkey Encryption guides |
| `scripts/copy-zk-artifacts.mjs` | Copies the `DataRegistry` contract's ZK artifacts into `public/` before `npm run dev` |
| `vite.config.ts`                | Vite plugins the Midnight SDK needs in the browser (WASM, top-level await, Node polyfills) |

## Following along with the guides

| Guide                                                                                   | Entry point    | Run with      |
| --------------------------------------------------------------------------------------- | -------------- | ------------- |
| [Mock Adapters](https://dstorage.pro/docs/guide/mock-adapters.html)                          | `src/index.ts` | `npm start`   |
| [Core Concepts](https://dstorage.pro/docs/guide/core-concepts.html)                          | conceptual only | (nothing to run) |
| [Local & Simulator Adapters](https://dstorage.pro/docs/guide/local-simulator-adapters.html)  | `src/index.ts` | `npm start`   |
| [Managed Payments Service](https://dstorage.pro/docs/guide/managed-payments-service.html)    | `src/index.ts` | `npm start`   |
| [Midnight Network Adapter](https://dstorage.pro/docs/guide/midnight-network-adapter.html)    | `src/main.ts`  | `npm run dev` |
| [Passkey Encryption](https://dstorage.pro/docs/guide/passkey-encryption.html)                | `src/main.ts`  | `npm run dev` |

### Node.js guides

Each Node.js guide uses a different combination of adapters, but `main()` keeps the same shape:
configure, `init()`, `store()`, `retrieveByRefId()`, `destroy()`. Replace the adapters in
`src/index.ts` with the ones from the guide you're on. Some guides need local services, such as
[arlocal](https://github.com/textury/arlocal); each guide's Prerequisites section lists them.

### Browser guides

The Midnight Network Adapter and Passkey Encryption guides run in the browser, because they
connect to a Midnight wallet extension (1AM by default, or Lace):

```bash
npm run dev
```

This copies the compiled `DataRegistry` contract's ZK artifacts into `public/`, starts a Vite dev
server, and serves a page with a **Run** button. The button runs the same `init()` → `store()` →
`retrieveByRefId()` sequence. Before you click it, set up the proof server, arlocal, and the
wallet as described in the guide's Prerequisites section.

`npm run build` creates a production bundle in `dist/`.

## Credentials

Never commit secrets such as a dStorage Pro auth token (used by the Managed Payments Service
guide). Load them from environment variables instead, for example
`authToken: process.env.DSTORAGE_AUTH_TOKEN`. `.env` files are already gitignored.

## License

[MIT](LICENSE)
