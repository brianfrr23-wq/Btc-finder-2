# BTC Finder

A small, mobile-friendly Bitcoin mainnet public-address checker, based on the uploaded BTC Finder preview.

## Features

- Check up to 10 supplied public addresses per search.
- Show confirmed balances, pending net changes and transaction counts.
- Show up to 25 recent transactions for an address.
- Save a named watchlist in this browser's local storage.
- Export successfully checked balances to CSV with timestamps.
- Link directly to Blockstream Explorer.

There is no private-key search, seed vault, recovery engine or spending feature. A dormant address is not proof of lost funds. The original upload was a nonfunctional interface preview; this version implements public-address lookup.

## Run

Open `index.html` in a modern browser with internet access, or serve this directory with `python3 -m http.server 8000` and open `http://localhost:8000`.

## GitHub Pages

In this repository, open **Settings → Pages**. Choose **Deploy from a branch**, then **main** and **/ (root)**, and save. GitHub will display the live app URL when deployment completes. Uploading code alone does not enable Pages.

## Data and privacy

Requests go directly from the browser to [Blockstream's Esplora API](https://github.com/Blockstream/esplora/blob/master/API.md). That provider receives the searched addresses and normal network information, including your IP address. This repository has no server or analytics. Saved watchlists stay in local browser storage and are not synced between devices. Clearing browser storage removes them. No seed phrases or credentials should be entered.

Balances are calculated in satoshis from funded outputs minus spent outputs. Confirmed balance and pending net change are shown separately. All addresses must be Bitcoin mainnet addresses; the explorer checks final validity. No data is fetched automatically at startup. API outages, browser restrictions and rate limits can prevent live searches. Failed requests are shown as errors, never as zero balances.

## Validation

Node checks with a simulated DOM and API cover successful responses, pending spending, invalid input, transactions, watchlist saving, duplicate prevention, rate limits and malformed responses. A live example address request also returned the expected API fields. Full browser and mobile visual checks were unavailable because the browser download failed in the build environment.
