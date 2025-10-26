# ElizaOS Plugins Report for Sendo

## Summary

This report catalogs the available actions from ElizaOS plugins for integration into Sendo project. 
All plugins analyzed are compatible with ElizaOS v1.

**Covered Plugins:**
- [plugin-jupiter](#plugin-jupiter) – Solana DEX aggregator for token swaps with optimal routing
- [plugin-pyth-data](#plugin-pyth-data) – Real-time price feeds and oracle data from Pyth Network
- [plugin-dexscreener](#plugin-dexscreener) – Multi-chain DEX analytics and token discovery
- [plugin-orca](#plugin-orca) – Solana Whirlpool concentrated liquidity management
- [plugin-meteora](#plugin-meteora) – Meteora DLMM (Dynamic Liquidity Market Maker) position automation
- [plugin-raydium](#plugin-raydium) – Raydium AMM and concentrated liquidity pool management

---

## [plugin-jupiter](https://github.com/elizaos-plugins/plugin-jupiter)

### Onchain Actions

- `getQuoteWithRetry(url, retries, delay)`
	- Fetches Jupiter quote with automatic retry and rate limit handling (429 errors). Uses exponential backoff.

- `quoteEnqueue(url)`
	- Adds quote request to queue to respect API rate limits (1 req/s).

- `getSwapWithRetry(url, payload, retries, delay)`
	- Executes swap with retry logic and rate limit handling.

- `getQuote({inputMint, outputMint, amount, slippageBps})`
	- Gets swap quote for token pair with caching and lamports estimation.

- `executeSwap({quoteResponse, userPublicKey, slippageBps})`
	- Executes token swap via Jupiter DEX with platform fees and compute units.

### Onchain Data

- `getTokenPrice(tokenMint, quoteMint, inputDecimals)`
	- Gets token price in USDC by performing a test swap.

- `getTokenPair({inputMint, outputMint})`
	- Fetches token pair information including liquidity and 24h volume.

- `getHistoricalPrices({inputMint, outputMint, timeframe})`
	- Gets historical price data for token pair over specified timeframe.

- `getCacheExp(runtime, key)`
	- Gets cached data with expiration check.

- `setCacheExp(runtime, key, val, ttlInSecs)`
	- Sets cached data with TTL expiration.

## [plugin-pyth-data](https://github.com/elizaos-plugins/plugin-pyth-data)

### Onchain Data

- `GET_LATEST_PRICE_UPDATES`
	- Retrieves latest price updates from Pyth Network with USD conversions and confidence intervals. Supports hex or base64 encoding.

- `GET_LATEST_PUBLISHER_CAPS`
	- Fetches latest publisher stake caps from Pyth Network showing publisher capabilities and limitations.

- `GET_PRICE_FEEDS`
	- Retrieves price feeds matching specific criteria with metadata (asset type, symbol, description).

- `GET_PRICE_UPDATES_STREAM`
	- Creates EventSource stream for real-time price updates with automatic data collection and formatting.

## [plugin-dexscreener](https://github.com/elizaos-plugins/plugin-dexscreener)

### Onchain Actions

- `search({query})`
	- Search for tokens/pairs across all DEXs and chains. Returns up to 5 results with pricing, volume, liquidity and DEX information.

- `getTokenInfo({tokenAddress})`
	- Get detailed information about a specific token (requires 0x address). Returns all trading pairs with comprehensive metrics including price, 24h change, volume, market cap and FDV.

- `getTrending({timeframe, limit})`
	- Get trending tokens based on timeframe (1h/6h/24h). Returns pairs with price changes, trading volume, market cap and buy/sell transaction counts.

- `getNewPairs({chain, limit})`
	- Find newly created trading pairs. Optionally filter by blockchain. Displays creation timestamps, prices and liquidity metrics.

- `getChainPairs({chain, sortBy, limit})`
	- Get top trading pairs from specific blockchain (Ethereum, BSC, Polygon, Arbitrum, Optimism, Base, Solana, Avalanche). Supports sorting by volume, liquidity, price change or transactions.

- `getBoostedTokens()`
	- Get boosted/promoted tokens from DexScreener with boost amounts and descriptions.

- `getTokenProfiles()`
	- Get latest token profiles with comprehensive metadata.

## [plugin-orca](https://github.com/elizaos-plugins/plugin-orca)

### Onchain Actions

- `managePositions({repositionThresholdBps, intervalSeconds, slippageToleranceBps})`
	- Automatically rebalances Solana Whirlpool LP positions when they drift beyond specified thresholds. Handles close and reopen operations with retry logic.

### Providers

- `positionProvider()`
    - Load wallet and fetch positions with the `fetchPositions(connection, ownerAddress)` method

## [plugin-meteora](https://github.com/elizaos-plugins/plugin-meteora)

### Onchain Actions

- `managePositions({repositionThresholdBps, slippageToleranceBps})`
	- Automates Meteora DLMM liquidity position rebalancing. Removes liquidity from drifted positions and creates new positions centered around active bin using SpotBalanced strategy.

### Providers

- `meteoraPositionProvider()`
    - Load wallet and fetch positions with the `fetchPositions(connection, ownerAddress)` method

## [plugin-raydium](https://github.com/elizaos-plugins/plugin-raydium)

### Onchain Actions

- `managePositions({repositionThresholdBps, intervalSeconds, slippageToleranceBps})`
	- Orchestrates automated rebalancing of Raydium liquidity positions when they drift beyond specified thresholds. Executes close-and-reopen cycles with retry logic.

### Providers

- `positionProvider()`
    - Load wallet and fetch positions with the `fetchPositions(connection, ownerAddress)` method

## [plugin-solana](https://github.com/elizaos-plugins/plugin-solana)

### Onchain Actions

- `executeSwap({inputTokenSymbol, outputTokenSymbol, inputTokenCA, outputTokenCA, amount})`
	- **Description**: Performs token swap via Jupiter aggregator. Resolves contract addresses from wallet holdings, validates parameters, signs and sends transaction to Solana mainnet.
	- **Aliases**: SWAP_TOKENS, TOKEN_SWAP, TRADE_TOKENS, EXCHANGE_TOKENS

- `transferToken({tokenAddress, recipient, amount})`
	- **Description**: Transfers SPL tokens from agent's wallet to another address. Manages Associated Token Accounts, creates recipient's ATA if needed, constructs versioned transaction.
	- **Aliases**: TRANSFER_TOKEN, TRANSFER_TOKENS, SEND_TOKENS, PAY_TOKEN, PAY_TOKENS, PAY

### Providers

- `walletProvider()`
    - Load each token data holded by the wallet and generate a `text` md variable 
