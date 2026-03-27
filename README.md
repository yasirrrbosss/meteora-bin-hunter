# 🌊 Meteora DLMM Bot

Private Telegram bot for fast Meteora DLMM liquidity management on Solana. Built for hit-and-run LP strategies.

## Features

- ⚡ **Auto LP** — paste pool link directly in chat, instantly adds liquidity using active preset
- 💼 **Multi-wallet** — import and switch wallets via Telegram, no code changes needed
- ⚡ **Strategy Presets** — save named presets with SOL amount, range%, and strategy. Supports `max` to auto-use 99% of wallet balance
- 📋 **Multi-strat input** — add multiple presets at once, one per line
- 🗑️ **Fast Remove** — `skipPreflight` + parallel transactions for speed
- 🔄 **Sync Positions** — detect positions opened manually on Meteora, auto-remove closed ones
- 🌐 **Auto Best RPC** — pings configured RPCs on startup, uses fastest one
- 💾 **Persistent** — wallets, positions, and presets saved to `data.json`
- 🎛️ **All-button UI** — everything via inline buttons, no manual commands needed

## Requirements

- Node.js v20+
- Telegram bot token from [@BotFather](https://t.me/BotFather)

## Installation

```bash
git clone https://github.com/dotnaonweh/meteora-dlmm-bot.git
cd meteora-dlmm-bot
npm install @meteora-ag/dlmm @solana/web3.js bn.js bs58
```

## Running

**With PM2 (recommended):**
```bash
npm install -g pm2
TELEGRAM_TOKEN=xxx WALLET_PRIVATE_KEY=xxx pm2 start meteorabot.js --name meteorabot
pm2 save
pm2 startup
```

**Direct:**
```bash
TELEGRAM_TOKEN=xxx WALLET_PRIVATE_KEY=xxx node meteorabot.js
```

## Environment Variables

| Variable | Required | Description |
|---|---|---|
| `TELEGRAM_TOKEN` | ✅ | Bot token from @BotFather |
| `WALLET_PRIVATE_KEY` | Optional | Base58 private key, loaded as "Default" wallet on first run |

## Usage

Send `/start` to your bot — everything is button-based.

### Auto Mode
Paste a Meteora pool link directly in chat:
```
https://app.meteora.ag/dlmm/POOL_ADDRESS
```
Instantly adds LP using your active strategy preset.

### Strategy Presets
Default preset `sannastrat` is always available. Add custom presets via **⚡ Strategy** → **➕ Tambah Strat**.

Supports single or multi-line input:
```
SETORANSPOT max 7 spot
SETORANBA max 7 bidask
SAFE 1 30 spot
```
Format: `name sol|max range% spot|curve|bidask`

Using `max` as SOL amount will automatically use 99% of the active wallet's balance.

### Wallet Management
Go to **💼 Wallet** → **➕ Import Wallet Baru** → send your private key in chat.

> ⚠️ Always delete the message containing your private key after sending!

### Sync Positions
Use **🔄 Sync Posisi** to detect positions opened manually on the Meteora website. Also removes positions that no longer exist on-chain.

## RPC Configuration

Edit `RPC_LIST` in `meteorabot.js`:

```js
const RPC_LIST = [
  { label: 'Helius', url: 'https://mainnet.helius-rpc.com/?api-key=YOUR_KEY' },
  { label: 'Solana Public', url: 'https://api.mainnet-beta.solana.com' },
  { label: 'Helius Pump', url: 'https://pump.helius-rpc.com/' },
];
```

## Security

- `data.json` contains wallet private keys — never commit it (already in `.gitignore`)
- Use a dedicated wallet, not your main wallet
- Always delete Telegram messages containing private keys after sending

## License

MIT
