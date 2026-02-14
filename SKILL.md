# Portfolio Tracker Skill

Track crypto portfolio value, P&L, and allocation using Strykr Prism API.

## When to Use

- User asks about their crypto holdings value
- User wants to check portfolio P&L
- User needs current prices for multiple tokens
- User wants allocation breakdown

## Usage

### Quick Price Check
```javascript
const { getPrice } = require('@strykr/portfolio-tracker');
const btc = await getPrice('BTC');
console.log(`BTC: $${btc.price}`);
```

### Track Portfolio
```javascript
const { PortfolioTracker } = require('@strykr/portfolio-tracker');

const portfolio = new PortfolioTracker();
portfolio.addHolding('BTC', 1.5, 45000);  // symbol, amount, cost basis
portfolio.addHolding('ETH', 10);

const valuation = await portfolio.getValuation();
// Returns total value, P&L, allocation per asset
```

### CLI
```bash
portfolio price BTC
portfolio track BTC:1.5 ETH:10 SOL:100
```

## API Endpoints Used

- `GET /crypto/price/{symbol}` - Single price
- `GET /batch/crypto/prices?symbols=X,Y,Z` - Batch prices

## Notes

- No API key required for basic usage
- Prices are real-time from Prism API
- Supports 10,000+ tokens across all chains

## Source

- NPM: `npm install @strykr/portfolio-tracker`
- GitHub: https://github.com/Strykr-Ai/portfolio-tracker
- API: https://prismapi.ai
