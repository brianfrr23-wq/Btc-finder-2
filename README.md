# LostBTC Hunter

A mobile-friendly, public Bitcoin mainnet activity explorer based on Brian's supplied interface. Published with GitHub Pages from `main` / repository root.

## Features

- Famous addresses: the eight addresses in the supplied historical list, with live balances and activity checks.
- Top holders: query Blockchair for 10–200 addresses ordered by balance; optional API key.
- Paste list: check up to 200 public addresses, deduplicated before requests.
- Adjustable dormancy threshold from 1–20 years and a dormant, unlabelled filter.
- Confirmed balances and pending net changes displayed separately.
- Summary totals by supplied address category, with failed and unknown-activity counts.
- CSV export of all attempted addresses, timestamps and lookup status.
- Stop a scan, save named addresses, and view up to 25 recent transactions.
- Existing BTC Finder watchlists are preserved under the same local-storage key.

## Interpretation

Dormancy requires a positive confirmed balance, a successful activity lookup and confirmed activity older than the threshold. Pending activity is treated as active. Failed activity checks remain unknown and are excluded from dormant totals. No transaction history is not treated as infinite dormancy. Incoming payments count as activity.

The supplied historical and exchange labels are unverified, and may be outdated or incorrect. They are not proof of ownership, missing keys or unspendability. An address's current balance is separate from any historical block reward associated with it. This app does not search private keys, recover wallets, store seed phrases, or spend funds.

## APIs and privacy

Public address requests go directly to [mempool.space](https://mempool.space/docs/api/rest). The top-holder list goes to [Blockchair](https://github.com/Blockchair/Blockchair.Support/blob/master/API_DOCUMENTATION_EN.md). Providers receive the query and normal network information, including the browser's IP address. No analytics or server is included.

Blockchair can reject unauthenticated requests, deny browser access, enforce plan limits or rate limit requests. Errors are shown rather than silently switching sources or reporting empty results as successful. A key may be required; no key is bundled. Top-holder responses were denied from the build environment with code 430, so a successful live top-holder query could not be verified.

The optional key remains in the current page unless the user checks **Remember key on this device**. Remembered keys are stored unencrypted in browser local storage, sent only to Blockchair, and excluded from exports. Unchecking the option removes the saved key. Watchlists remain on the current device and are not synced.

## Run and deploy

Open `index.html` in a modern browser, or serve this directory using `python3 -m http.server 8000`. Internet access is required for live data. GitHub Pages is configured to deploy from the `main` branch root.

## Validation

Node tests with a simulated DOM and API cover preserved watchlists, duplicate removal, invalid input, confirmed dormancy, pending activity, unknown activity, failure displays, CSV escaping, top-list denials, control bounds, opt-in key storage and stopping scans. Live browser verification is performed after deployment.
