# @strykr/portfolio-tracker

Real-time crypto portfolio tracker powered by [Strykr Prism API](https://prismapi.ai). Track holdings, P&L, and allocation across Bitcoin, Ethereum, Solana, and 10,000+ tokens.

## Features

- 📊 **Real-time prices** from Prism API (no API key required)
- 💰 **Portfolio valuation** with P&L tracking
- 📈 **24h change** for each holding
- 🎯 **Allocation percentages** auto-calculated
- 🖥️ **CLI included** for quick lookups
- ⚡ **Zero dependencies** - just native fetch

## Installation

```bash
npm install @strykr/portfolio-tracker
```

## Quick Start

```javascript
const { PortfolioTracker, getPrice } = require('@strykr/portfolio-tracker');

// Single price lookup
const btc = await getPrice('BTC');
console.log(`Bitcoin: $${btc.price}`);

// Track a portfolio
const portfolio = new PortfolioTracker();
portfolio
  .addHolding('BTC', 1.5, 45000)  // 1.5 BTC @ $45k cost basis
  .addHolding('ETH', 10, 2500)    // 10 ETH @ $2.5k cost basis
  .addHolding('SOL', 100);        // 100 SOL, no cost basis

const valuation = await portfolio.getValuation();
console.log(`Total: $${valuation.totalValue.toLocaleString()}`);
console.log(`P&L: $${valuation.totalPnl.toLocaleString()}`);
```

## CLI Usage

```bash
# Get current price
portfolio price BTC
portfolio price ETH

# Track portfolio value
portfolio track BTC:1.5 ETH:10 SOL:100
```

## API Reference

### `PortfolioTracker`

```javascript
const tracker = new PortfolioTracker({ apiKey: 'optional' });

// Add holdings
tracker.addHolding(symbol, amount, costBasis?)

// Remove holdings
tracker.removeHolding(symbol, amount?)

// Get valuation
const result = await tracker.getValuation();
// Returns: { totalValue, totalPnl, holdings: [...] }

// Serialize
const json = tracker.toJSON();
const restored = PortfolioTracker.fromJSON(json);
```

### `getPrice(symbol)`

Quick lookup for a single token.

```javascript
const { getPrice } = require('@strykr/portfolio-tracker');
const data = await getPrice('BTC');
// { price: 67500, change_24h: 2.5, ... }
```

### `getPrices(symbols)`

Batch lookup for multiple tokens.

```javascript
const { getPrices } = require('@strykr/portfolio-tracker');
const prices = await getPrices(['BTC', 'ETH', 'SOL']);
```

## Response Format

```javascript
{
  totalValue: 125000,
  totalCost: 100000,
  totalPnl: 25000,
  totalPnlPercent: 25,
  holdings: [
    {
      symbol: 'BTC',
      amount: 1.5,
      price: 67500,
      value: 101250,
      costBasis: 45000,
      pnl: 33750,
      pnlPercent: 50,
      allocation: 81,
      change24h: 2.5
    },
    // ...
  ],
  timestamp: '2024-02-14T10:30:00.000Z'
}
```

## Environment Variables

| Variable | Description |
|----------|-------------|
| `PRISM_API_KEY` | Optional API key for higher rate limits |

## Supported Assets

- **Crypto**: BTC, ETH, SOL, and 10,000+ tokens across all major chains
- **DeFi**: LP tokens, staked positions, wrapped assets
- **Real-time**: Prices update every few seconds

## Powered by Strykr Prism

[Prism API](https://prismapi.ai) provides unified financial data for AI agents and developers:
- Crypto prices across 50+ chains
- Stock quotes and fundamentals
- DeFi protocols and yields
- Prediction markets
- Sports betting odds

## License

MIT
