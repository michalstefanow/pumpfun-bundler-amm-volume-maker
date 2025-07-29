# Pumpfun AMM Bundler & Volume Maker

## Overview

The Pumpfun AMM Bundler & Volume Maker is an automated trading tool designed for Pumpfun and Raydium on the Solana blockchain. This bot allows users to efficiently create liquidity pools, bundle transactions, and increase trading volume strategically. By leveraging Jito bundling, it ensures swift execution of transactions, making it a powerful tool for market making and liquidity management.

## Features

- **Pool Creation & Bundling**: Automates the creation of new liquidity pools and bundles transactions for efficiency
- **Jito Bundling**: Utilizes Jito bundling to ensure transactions are executed in the first block
- **Volume Management**: Simulates organic trading volume to enhance liquidity
- **Multi-Wallet Support**: Manages multiple wallets to distribute trades and maintain anonymity
- **Customizable Trading Strategies**: Allows users to configure strategies for market-making and sniping
- **Efficient & Fast Execution**: Optimized for speed to gain an edge in high-frequency trading environments
- **SOL Distribution**: Automatically distributes SOL across multiple wallets for trading
- **Token Gathering**: Collects tokens and SOL back to the main wallet after trading cycles

## Prerequisites

Ensure you have the following installed:
- Node.js (v16+)
- npm or yarn
- Solana CLI & Keypair
- Pumpfun AMM access

## Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/michalstefanow/pumpfun-bundler-amm-volume-maker.git
   cd pumpfun-amm-bundler-volume-maker
   ```

2. **Install dependencies**
   ```bash
   npm install
   # or
   yarn install
   ```

3. **Set up environment variables**
   Create a `.env` file in the root directory with the following variables:
   ```env
   # Wallet Configuration
   PRIVATE_KEY=your_main_wallet_private_key
   
   # RPC Configuration
   RPC_ENDPOINT=your_solana_rpc_endpoint
   RPC_WEBSOCKET_ENDPOINT=your_solana_websocket_endpoint
   
   # Trading Configuration
   TOKEN_MINT=target_token_mint_address
   SLIPPAGE=1.0
   
   # Distribution Settings
   DISTRIBUTE_WALLET_NUM=10
   SOL_AMOUNT_TO_DISTRIBUTE=0.1
   DISTRIBUTE_INTERVAL_MIN=30
   DISTRIBUTE_INTERVAL_MAX=60
   
   # Buy Settings
   BUY_UPPER_PERCENT=80
   BUY_LOWER_PERCENT=20
   BUY_INTERVAL_MIN=5
   BUY_INTERVAL_MAX=15
   
   # Sell Settings
   SELL_INTERVAL_MIN=10
   SELL_INTERVAL_MAX=30
   
   # Jito Configuration
   JITO_MODE=true
   JITO_FEE=1000000
   ```

## Usage

### Starting the Volume Bot

Run the main volume bot:
```bash
npm start
# or
yarn start
```

### Gathering Tokens and SOL

After trading cycles, gather all tokens and SOL back to the main wallet:
```bash
npm run gather
# or
yarn gather
```

## Configuration

### Environment Variables

| Variable | Description | Default | Required |
|----------|-------------|---------|----------|
| `PRIVATE_KEY` | Main wallet private key | - | Yes |
| `RPC_ENDPOINT` | Solana RPC endpoint | - | Yes |
| `RPC_WEBSOCKET_ENDPOINT` | Solana WebSocket endpoint | - | Yes |
| `TOKEN_MINT` | Target token mint address | - | Yes |
| `SLIPPAGE` | Trading slippage percentage | 1.0 | No |
| `DISTRIBUTE_WALLET_NUM` | Number of wallets to distribute SOL to | 10 | No |
| `SOL_AMOUNT_TO_DISTRIBUTE` | SOL amount to distribute per wallet | 0.1 | No |
| `DISTRIBUTE_INTERVAL_MIN` | Minimum interval between distributions (seconds) | 30 | No |
| `DISTRIBUTE_INTERVAL_MAX` | Maximum interval between distributions (seconds) | 60 | No |
| `BUY_UPPER_PERCENT` | Maximum percentage of wallet balance to buy | 80 | No |
| `BUY_LOWER_PERCENT` | Minimum percentage of wallet balance to buy | 20 | No |
| `BUY_INTERVAL_MIN` | Minimum wait time between buys (seconds) | 5 | No |
| `BUY_INTERVAL_MAX` | Maximum wait time between buys (seconds) | 15 | No |
| `SELL_INTERVAL_MIN` | Minimum wait time before selling (seconds) | 10 | No |
| `SELL_INTERVAL_MAX` | Maximum wait time before selling (seconds) | 30 | No |
| `JITO_MODE` | Enable Jito bundling | true | No |
| `JITO_FEE` | Jito bundle fee in lamports | 1000000 | No |

## Project Structure

```
pumpfun-amm-bundler-volume-maker/
├── index.js              # Main volume bot entry point
├── gather.js             # Token and SOL gathering script
├── package.json          # Project dependencies and scripts
├── README.md            # Project documentation
├── .gitignore           # Git ignore rules
├── constants/           # Configuration constants
│   ├── constants.js     # Environment variable definitions
│   └── index.js         # Constants exports
├── utils/               # Utility functions
│   ├── utils.js         # General utility functions
│   ├── swapOnlyAmm.js   # AMM swap functionality
│   └── index.js         # Utils exports
└── executor/            # Transaction execution modules
    ├── jito.js          # Jito bundling execution
    └── legacy.js        # Standard transaction execution
```

## How It Works

1. **SOL Distribution**: The bot distributes SOL from the main wallet to multiple sub-wallets
2. **Trading Cycle**: Each sub-wallet performs buy and sell operations with configurable intervals
3. **Volume Generation**: Multiple wallets trading simultaneously creates organic-looking volume
4. **Token Gathering**: After trading cycles, all tokens and remaining SOL are collected back to the main wallet

## Key Components

### Main Bot (`index.js`)
- Manages SOL distribution across multiple wallets
- Orchestrates buy/sell cycles with random intervals
- Handles error recovery and retry logic

### Gather Script (`gather.js`)
- Collects all tokens from sub-wallets
- Transfers remaining SOL back to main wallet
- Closes token accounts to save rent

### Jito Integration (`executor/jito.js`)
- Provides fast transaction execution through Jito bundling
- Ensures transactions are included in the first block
- Optimizes for high-frequency trading scenarios

## Security Considerations

- **Private Keys**: Never commit your `.env` file or expose private keys
- **RPC Limits**: Be aware of RPC rate limits when running multiple instances
- **Network Fees**: Monitor SOL balance for transaction fees
- **Slippage**: Configure appropriate slippage to avoid failed transactions

## Troubleshooting

### Common Issues

1. **Insufficient SOL Balance**
   - Ensure main wallet has enough SOL for distribution and fees
   - Check `SOL_AMOUNT_TO_DISTRIBUTE` configuration

2. **RPC Connection Issues**
   - Verify RPC endpoint is accessible
   - Consider using a premium RPC service for better reliability

3. **Transaction Failures**
   - Check slippage settings
   - Ensure token mint address is correct
   - Verify wallet has sufficient balance

4. **Jito Bundle Failures**
   - Increase Jito fee if bundles are being rejected
   - Check Jito network status

## Contact

Have any questions or need help? Contact here:
- [Telegram](https://t.me/mylord1_1)
- [Twitter](https://x.com/michalstefanow)

## License

This project is for educational and research purposes. Use at your own risk and ensure compliance with local regulations.
