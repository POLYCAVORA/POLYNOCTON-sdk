# 🚀 Quick Start - PolyEmperion SDK v0.2.0

Welcome! This SDK is now **ready to use** for building Polymarket trading applications!

---

## 📦 What's New in v0.2.0

✅ **Full Trading Support** - Place, cancel, and manage orders  
✅ **CLOB Integration** - Direct integration with Polymarket's CLOB  
✅ **Backend & Frontend Modes** - For bots and web apps  
✅ **Builder Support** - Attribute orders to your builder account  
✅ **Comprehensive Docs** - Guides, examples, and FAQs  

---

## 🎯 Getting Started (3 Easy Steps)

### Step 1: Install the SDK

```bash
npm install @PolyEmperion/sdk
```

### Step 2: Choose Your Use Case

#### Option A: Data Only (No Trading)

```typescript
import { PolyEmperionSDK } from "@PolyEmperion/sdk";

const sdk = new PolyEmperionSDK();

// Fetch markets
const markets = await sdk.getMarkets();
console.log(`Found ${markets.length} markets`);

// Get specific market
const market = await sdk.getMarket("market-id");
console.log(market.question);
```

#### Option B: Trading (Backend/Bot)

```typescript
import { PolyEmperionSDK } from "@PolyEmperion/sdk";

const sdk = new PolyEmperionSDK({
  trading: {
    chainId: 137, // Polygon mainnet
    backend: {
      privateKey: process.env.PRIVATE_KEY, // Your wallet's private key
    },
  },
});

// Initialize trading
const trading = sdk.trading.init();

// Place an order
const order = await trading.placeOrder({
  tokenId: "0x123...", // Get from market data
  side: "BUY",
  price: 0.65, // 65 cents
  size: 10, // 10 shares
});

console.log("Order placed:", order.orderId);

// Get open orders
const orders = await trading.getOpenOrders();
console.log(`You have ${orders.length} open orders`);

// Cancel an order
await trading.cancelOrder(order.orderId);
```

#### Option C: Trading (Frontend/Web App)

```typescript
import { PolyEmperionSDK } from "@PolyEmperion/sdk";
import { ethers } from "ethers";

// Connect to user's wallet
const provider = new ethers.providers.Web3Provider(window.ethereum);
await provider.send("eth_requestAccounts", []);
const signer = provider.getSigner();

// Initialize SDK
const sdk = new PolyEmperionSDK({
  trading: {
    chainId: 137,
    frontend: {
      signer: signer,
    },
  },
});

const trading = sdk.trading.init();

// User signs and places order
const order = await trading.placeOrder({
  tokenId: "0x123...",
  side: "BUY",
  price: 0.65,
  size: 10,
});
```

### Step 3: Run Your Code

```bash
# For data/streaming
node your-script.js

# For trading (with private key from env)
PRIVATE_KEY=0x... node your-trading-bot.js
```

---

## 📚 Documentation

### For Beginners
👉 **[GUIDE_FOR_NEWBIES.md](./GUIDE_FOR_NEWBIES.md)** - Complete beginner's guide (500+ lines!)

### For Everyone
👉 **[README.md](./README.md)** - Full API reference and documentation

### Examples
👉 **[examples/list-markets.ts](./examples/list-markets.ts)** - Fetch markets  
👉 **[examples/live-orderbook.ts](./examples/live-orderbook.ts)** - Stream orderbook  
👉 **[examples/trading-example.ts](./examples/trading-example.ts)** - Trading example  

### Summary
👉 **[IMPLEMENTATION_SUMMARY.md](./IMPLEMENTATION_SUMMARY.md)** - What changed in v0.2.0

---

## ⚠️ Important Security Notes

**NEVER do this:**
- ❌ Put your private key in your code
- ❌ Commit private keys to git
- ❌ Use private keys in frontend/browser code

**ALWAYS do this:**
- ✅ Use environment variables: `process.env.PRIVATE_KEY`
- ✅ Add `.env` to your `.gitignore` (already done ✓)
- ✅ Use backend mode only on secure servers
- ✅ Use frontend mode for web apps (users control their keys)

**Example .env file:**
```
PRIVATE_KEY=0x1234567890abcdef...
BUILDER_KEY=your-builder-key
BUILDER_SECRET=your-builder-secret
BUILDER_PASSPHRASE=your-builder-passphrase
```

---

## 🤔 FAQ

### "Is this SDK only for data/streaming?"
**No!** This SDK now has THREE features:
1. Data fetching (markets, odds)
2. Real-time streaming (orderbook updates)
3. **Trading** (place, cancel, manage orders) - NEW!

### "Do I need builder credentials?"
**No, they're optional.** Builder credentials are for:
- Order attribution and analytics
- Potential fee rebates
- Building reputation as a market maker

Contact Polymarket to get builder credentials if you want them.

### "Backend vs Frontend mode?"
- **Backend mode** = For bots/servers with private key
- **Frontend mode** = For web apps where users connect wallets

### "Do I need USDC?"
**Yes**, you need USDC on Polygon network to trade.

### "Is there a testnet?"
Polymarket is on Polygon mainnet. Start with small amounts to test!

---

## 🛠️ Run the Examples

```bash
# 1. List all markets
npm run examples:list

# 2. Stream live orderbook (set market ID)
PolyEmperion_MARKET_ID=<market-id> npm run examples:orderbook

# 3. Trading example (set your private key)
PRIVATE_KEY=0x... npm run examples:trading
```

---

## 🎯 What Can You Build?

### Beginner Projects
- 📊 Market dashboard showing current odds
- 📈 Price tracker with historical data
- 🔔 Alert system for price changes

### Intermediate Projects
- 🤖 Trading bot with custom strategies
- 💹 Market maker providing liquidity
- 🔍 Arbitrage scanner

### Advanced Projects
- 🧠 AI-powered trading agent
- 🌐 Complete trading platform
- 📊 Analytics and insights dashboard

---

## 💻 Need Help?

### Resources
- **Full Guide**: [GUIDE_FOR_NEWBIES.md](./GUIDE_FOR_NEWBIES.md)
- **API Docs**: [README.md](./README.md)
- **Examples**: [examples/](./examples/)

### Community
- **GitHub Issues**: https://github.com/PolyEmperion/PolyEmperion-sdk/issues
- **X (Twitter)**: [@polyemperion](https://x.com/polyemperion)
- **Website**: [polyemperion.xyz](https://polyemperion.xyz)

---

## ✅ Checklist Before You Start Trading

- [ ] SDK installed: `npm install @PolyEmperion/sdk`
- [ ] Private key saved in `.env` file
- [ ] `.env` is in `.gitignore` (already done ✓)
- [ ] USDC in your Polygon wallet
- [ ] Read the security warnings
- [ ] Tested with small amounts first

---

## 🚀 You're Ready!

The SDK is fully functional and ready to use. Start building your Polymarket trading application today!

**Happy building!** 🎉

---

**Version:** 0.2.0  
**Status:** ✅ Production Ready  
**License:** MIT
