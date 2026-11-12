# Flap Token — SPECS (BSC)

## What this is
A simple meme token launched ON Flap.sh (flap.sh), the #1 working BSC launchpad
right now. We do NOT build a launchpad. Flap deploys the token, runs the bonding
curve, and graduates it to PancakeSwap. Our build work here: metadata, image,
the Portal launch call, and the launch post.

## Verified launch facts (checked 2026-11-03 ~15:14 GMT)
- Flap Portal proxy (BSC chain 56): `0xe2cE6ab80874Fa9Fa2aAE65D277Dd6B8e65C9De0` (Portal v5.8.6)
- No contract to write, no launch fee, one signature. Fixed supply 1,000,000,000,
  all on a constant-product bonding curve with virtual reserves.
- Flap takes ~1% on every curve trade. Graduation: curve fills (Portal reads
  progress toward a 16 BNB threshold) → liquidity moves to PancakeSwap, curve closes.
- Tax: Flap launches tax tokens (min 1% per side per current guides; valid values
  1/3/5/10%). Tax goes to the creator's wallet (beneficiary) on every trade.
- Quote asset: BNB (or USD1). DEX graduation default: PancakeSwap V3.
- CREATE2 vanity address: tax tokens end in `7777` (standard `8888`); salt grind
  ~65k iterations, <1s. Predicted address known before sending.
- Gas ~0.003 BNB. Platform fee 0. (Third-party launch tools charge ~0.015 BNB
  service fee — do NOT use them; launch direct via the Portal call.)
- Metadata: name (max 50 chars), symbol (max 10 chars, UPPERCASE), image, short
  description, links. Image URL CANNOT be changed after launch — host on IPFS.
  Upload via `funcs.flap.sh/api/upload`, pass returned CID as `--meta`.
- Duels (Flap's PvP mechanic) activate at ~$24k market cap.
- Execution path for this user: encode the Portal `newTokenV5` call, preview with
  `baw contract-call preview`, user confirms, execute with `baw contract-call
  execute`. Same pattern as the contract withdraws (2026-11-03). The Binance
  Agentic Wallet cannot connect to flap.sh in a browser, so the baw route is it.
- Wallet session lapses ~2026-11-05 08:14 GMT — launch before then or re-sign in.

## LOCKED
- Chain: BSC (56). Portal: `0xe2cE6ab80874Fa9Fa2aAE65D277Dd6B8e65C9De0`.
- Supply: 1,000,000,000 (fixed by Flap). Quote: BNB.
- Tax: 1% buy / 1% sell, beneficiary = user wallet
  `0x75d251Ba39dED2E456d9f6DD776f77d422864403`.
- Dev buy: 0 (no funds to spare; wallet ~0.015 BNB, gas ~0.003 leaves ~0.012).
- No audit (Flap deploys a standard token; nothing custom to audit).

## Blue Tsunami — PICKED 2026-11-04 ~11:36 GMT
- Name: Blue Tsunami, symbol: BTSUNAMI (changed 2026-11-04 ~11:45 GMT from TSUNAMI — TSUNAMI was already used by dead 2022 BSC tokens; BTSUNAMI / TSUN26 / BTSU were checked by web search with no BSC token found; user picked BTSUNAMI). Midterm meme: Democrats flipped House + Senate Nov 3, 2026, "blue tsunami".
- Image: blue donkey surfing a blue wave, `blue-tsunami.png` (1600x1600). Pinata image CID `bafkreicu5jslflu3uhbya5srs76ntobpd4sh2qblpbvscruzocr445kwbm`. Flap meta CID `bafkreia23nozj6lgx5zj4dyogmicsc34ixqq2qyj6km5seef6nxkmetlyq` (via funcs.flap.sh/api/upload).
- Ticker collision: $TSUNAMI already exists on BSC as dead 2022 tokens (e.g. Tsunami Protocol 0xFD801a70156C4E254C86F112ac15F2a920a051B8, $0 liquidity/volume). Does not block a Flap launch, but buyers may confuse it with the old tokens.
- Launch path CORRECTED 2026-11-04: live Portal is v5.27.2 (not v5.8.6 in docs), implementation 0x6fc1ac64c90a5a6d9e7efc0d4064452af3fc9968. Only TAXED_V3 via `newTokenV6` works; `newTokenV5` taxDuration 0 reverts `TaxDurationTooShort()` (selector 0xaef851bb). Tax duration 365 days (31536000s) passes eth_call.
- Params (newTokenV6): dexThresh 1 (FOUR_FIFTHS, 80% graduation), migratorType 1 (V2_MIGRATOR), dexId 0, lpFeeProfile 0, buy/sell tax 100bps each, taxDuration 31536000, antiFarmerDuration 3600, mktBps 10000 / deflation 0 / dividend 0 / lp 0, minimumShareBalance 0, dividendToken 0x0, commissionReceiver 0x0, tokenVersion 6 (TAXED_V3), quoteToken 0x0 (native BNB), quoteAmt 0, value 0.
- CHANGED 2026-11-04 ~11:56 GMT — AI人生 split, user said "Do this for Btsunami": buy/sell tax 300bps each (3%), taxDuration 3153600000 (100 years), mktBps 5000 / deflationBps 2500 / dividendBps 2500 / lpBps 0, dividendToken WBNB 0xbb4CdB9CBd36B01bD1cBaEBF2De08d9173bc095c, minimumShareBalance 500,000 tokens (copied from AI人生, verified on-chain: its feeConfigV3 is 5000/0/0/0/2500/0/2500, dividendToken WBNB, minimumShareBalance 500,000, totalQuoteSentToMarketing 12.770746 BNB, totalQuoteSentToDividend 6.385373 BNB, dead balance 204,666,336 tokens). New preview requestId ae3feab4ab61494880492e308f81f19a, clean, gasLimit 6,000,000, eth_estimateGas 5,545,928. Predicted address unchanged 0x3aFf8890DA48DeE2433d88805a1ce8cB02567777. Awaiting explicit confirm to execute.
- LAUNCHED 2026-11-04 ~12:02 GMT, user confirmed "Let's try 3 percent": first preview ae3feab4 expired, re-previewed 2dd9b4dbbb2047829933b9c741aae707 (clean), executed — tx 0x3bbd2912baf52fca069944cfcce99ab0c83c5cfd45f0ea06659d6e12a865d04a, block 131621449, status 1, gasUsed 5,294,962, gas cost ~0.000458 BNB (wallet 0.014456 → 0.013998 BNB). Token VERIFIED on-chain: name Blue Tsunami, symbol BTSUNAMI, totalSupply 1,000,000,000, buy/sell tax 300/300 (3%/3%), feeConfigV3 mkt 5000 / deflation 2500 / dividend 2500 / lp 0, dividendToken WBNB, market wallet = user wallet. Status 1 = bonding curve, progress 0, no trades yet at verification. DexScreener pairs null at ~12:03 GMT (not indexed yet).
- Reference tokens checked on-chain 2026-11-04: BAN 0x848e2b1cb00dc439a15b03b8c3194e7d08917777 — 3%/3%, 100% burn (deflation 10000, mkt 0), dead 175.9M BAN; 我画地为牢 0x29921A532878bf66eFC9ca92694B8A40E6157777 — 0% buy / 1% sell, 100% dividends in FXIon, total distributed 130.960023 FXIon, mkt 0; AI人生 0x34257736852e866a7bf5B387b424fDeC92737777 — 3%/3%, 50% creator / 25% burn / 25% WBNB dividends (see above).
- Salt `0xf80371b0a498f4c98afeb2c1114ebde8c904d2d033a5abebb616e31af5036960`, predicted token `0x3aFf8890DA48DeE2433d88805a1ce8cB02567777` (ends 7777, 13,942 iterations). Token impl taxV3 `0x024f18294970B5c76c0691b87f138A0317156422`.
- Calldata in `blue-tsunami-launch.json`. eth_call simulation SUCCEEDS and returns the predicted address. eth_estimateGas 5,543,573 (~0x54a895).
- BLOCKED 2026-11-04 ~11:40 GMT: `baw contract-call preview` still fails with code 351805 "Transaction simulation failed: execution reverted", even though direct eth_call passes. No execute attempted. Next options: retry preview, try preview with an explicit gas limit (needs user approval — baw skill says gasLimit only on user request), or try an alternative launch route. Wallet session still lapses ~2026-11-05 08:14 GMT; DevMode enabled until 2026-11-10.


## OPEN — user picks
- Name, symbol, narrative, image direction.
- Suggestions offered 2026-11-03 ~15:15 GMT:
  1. Fox Duel (DUEL) — NFOX foxes + Flap PvP duels; ready-made fox audience.
  2. Flapjack (JACK) — Flap-native mascot play, fun and memorable.
  3. Agent Arena (ARENA) — AI agents battle in the arena; Agent ID world.

## Steps after the pick
1. Generate token image; pin image + metadata JSON to IPFS (Pinata, already
   connected) and/or upload via funcs.flap.sh/api/upload → CID.
2. Fetch Portal implementation ABI (BscScan/Sourcify) for `newTokenV5`.
3. Grind CREATE2 salt for `7777` suffix; compute predicted token address.
4. Build calldata; `baw contract-call preview` (value 0, gas only); show preview,
   user confirms; execute. Verify token on BscScan + flap.sh.
5. Draft launch post → X Post Drafts chat; user posts AT launch.

## Risks (honest)
- 355k launches/30d on Flap — attention is the scarce resource, not the build.
- Tax tokens: 1% each side is the minimum; higher tax would kill trading.
- If the wallet session lapses before launch, user must re-sign in (QR).
- Flap docs disagree on graduation detail (80% sold vs 16 BNB threshold) — verify
  live on the Portal read after launch.
- Do NOT promise returns, floor price, or airdrops. Token is a meme; say so.

## Related
- Research: `~/workspace/research_notes/latest-working-crypto-meta-nov-2026-20261103-1503/report.md`
- Playbook: `~/workspace/custom-skills/agent-mint-launch/SKILL.md` (gates pattern;
  this launch is simpler — no custom contract, Flap deploys it).
