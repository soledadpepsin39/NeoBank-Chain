# 🏗️ NeoBank Chain — Technical Architecture

> **Version 1.0 | April 2026**
> *Expert-level technical documentation for developers, auditors, and institutional partners*

---

## 📌 Table of Contents

1. [Architecture Overview](#1-architecture-overview)
2. [Why Solana 2026](#2-why-solana-2026)
3. [Core Innovation Stack](#3-core-innovation-stack)
4. [System Architecture](#4-system-architecture)
5. [Smart Contract Architecture](#5-smart-contract-architecture)
6. [CeFi Integration Layer](#6-cefi-integration-layer)
7. [DeFi Integration Layer](#7-defi-integration-layer)
8. [Security Architecture](#8-security-architecture)
9. [Data Architecture](#9-data-architecture)
10. [API Architecture](#10-api-architecture)
11. [Mobile Architecture](#11-mobile-architecture)
12. [Performance & Scalability](#12-performance--scalability)
13. [Code Standards & Patterns](#13-code-standards--patterns)

---

## 1. Architecture Overview

NeoBank Chain is built on a **hybrid architecture** that bridges
Centralized Finance (CeFi) and Decentralized Finance (DeFi)
through a unified, secure, and scalable infrastructure.

### 1.1 High-Level Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                     CLIENT LAYER                                 │
│   iOS App          Android App         Web App (future)         │
│   (React Native)   (React Native)      (React.js)               │
└──────────────────────────┬──────────────────────────────────────┘
                           │ HTTPS / WSS
┌──────────────────────────▼──────────────────────────────────────┐
│                     API GATEWAY                                  │
│         Rate Limiting | Auth | Load Balancing | Logging         │
│                   (AWS API Gateway)                              │
└──────┬───────────────────┬───────────────────┬──────────────────┘
       │                   │                   │
┌──────▼──────┐   ┌────────▼────────┐  ┌──────▼──────────────────┐
│  AUTH       │   │   CORE API      │  │   BLOCKCHAIN API         │
│  SERVICE    │   │   SERVICE       │  │   SERVICE                │
│             │   │                 │  │                          │
│ • JWT       │   │ • User mgmt     │  │ • Solana RPC             │
│ • KYC/AML   │   │ • Transactions  │  │ • Smart contracts        │
│ • Biometric │   │ • Notifications │  │ • DeFi protocols         │
│ • 2FA       │   │ • Analytics     │  │ • Wallet management      │
└──────┬──────┘   └────────┬────────┘  └──────┬───────────────────┘
       │                   │                   │
┌──────▼───────────────────▼───────────────────▼───────────────────┐
│                      DATA LAYER                                   │
│   PostgreSQL          Redis Cache          Solana Blockchain      │
│   (User data)         (Sessions/Queue)     (On-chain data)        │
└───────────────────────────────────────────────────────────────────┘
       │                                       │
┌──────▼──────────────────┐   ┌───────────────▼────────────────────┐
│   CeFi INTEGRATIONS     │   │   DeFi INTEGRATIONS                │
│                         │   │                                    │
│ • Stripe (cards)        │   │ • Jupiter (DEX aggregator)         │
│ • MoonPay (fiat ramp)   │   │ • Jito (liquid staking)            │
│ • SEPA / SWIFT          │   │ • Kamino (yield strategies)        │
│ • Jumio (KYC)           │   │ • Solend (lending)                 │
│ • Banking APIs          │   │ • Pyth (price oracles)             │
└─────────────────────────┘   └────────────────────────────────────┘
```

### 1.2 Design Principles

| Principle | Implementation |
|---|---|
| **Security First** | Zero-trust architecture, end-to-end encryption |
| **Non-Custodial Option** | Users control private keys via secure enclave |
| **Regulatory Compliance** | KYC/AML at protocol level via Solana ACE |
| **High Availability** | 99.99% uptime target, multi-region deployment |
| **Scalability** | Horizontal scaling, Solana's 65,000 TPS capacity |
| **Privacy** | JitoBAM encrypted mempool, GDPR compliant |

---

## 2. Why Solana 2026

### 2.1 Performance Comparison

| Metric | Bitcoin | Ethereum | Solana 2026 |
|---|---|---|---|
| TPS | 7 | 15–30 | **65,000+** |
| Finality | ~60 min | ~15 min | **~150ms** ⚡ |
| Avg Fee | $1–20 | $2–50 | **$0.00025** |
| Energy/tx | 700 kWh | 0.03 kWh | **0.00051 kWh** |
| Uptime 2025 | 99.9% | 99.9% | **100%** |

### 2.2 Solana 2026 Key Upgrades

#### 🔵 Alpenglow — Consensus Revolution
```
Previous Solana finality : ~12 seconds
Alpenglow finality       : ~150 milliseconds
Improvement              : 80x faster

Impact on NeoBank Chain:
→ Real-time payment confirmation
→ Instant cross-border transfers
→ Sub-second DeFi operations
→ Banking-grade transaction speed
```

#### 🟣 ACE — Application Controlled Execution
```
What it does:
→ Allows protocol-level KYC/AML checks before execution
→ Custom transaction ordering per application
→ Fair order flow control
→ Reduced MEV (Miner Extractable Value) risk

Impact on NeoBank Chain:
→ Compliance built into the blockchain layer
→ Regulatory requirements met at protocol level
→ Institutional-grade execution environment
→ Aligns with banking best-execution policies
```

#### 🟢 JitoBAM — Privacy & MEV Protection
```
What it does:
→ Encrypted mempool via Trusted Execution Environments (TEEs)
→ Transactions remain private until execution
→ Eliminates sandwich attacks
→ Transparent transaction sequencing

Impact on NeoBank Chain:
→ Users protected from front-running
→ Fair pricing on all swaps
→ Banking-grade transaction privacy
→ Trust layer for institutional users
```

### 2.3 Institutional Adoption (2026 Data)

```
Goldman Sachs    →  $108M in SOL holdings
BlackRock BUIDL  →  $550M cleared on Solana
Citigroup        →  Full trade finance lifecycle on-chain
Western Union    →  USD stablecoin launching on Solana H1 2026
Morgan Stanley   →  Filed SEC applications for SOL ETFs
Fidelity         →  Launched validator on Solana

Conclusion: The world's largest financial institutions
have validated Solana as institutional-grade infrastructure.
NeoBank Chain builds on this foundation.
```

---

## 3. Core Innovation Stack

### 3.1 The CeFi + DeFi Bridge — Technical Implementation

```
┌─────────────────────────────────────────────────────────────┐
│                    BRIDGE PROTOCOL                          │
│                                                             │
│  CeFi Request         Bridge Logic          DeFi Execution │
│  ─────────────        ────────────          ─────────────  │
│  "Send $100"    →     Route optimizer   →   USDC transfer  │
│  "Save money"   →     Yield selector    →   Kamino vault   │
│  "Get a loan"   →     Rate comparator   →   Solend borrow  │
│  "Buy crypto"   →     DEX aggregator    →   Jupiter swap   │
│                                                             │
│  The bridge always finds the BEST route:                   │
│  Cheapest + Fastest + Most Compliant                       │
└─────────────────────────────────────────────────────────────┘
```

### 3.2 Smart Routing Algorithm

```typescript
// Pseudocode — Smart routing logic
interface RouteOptions {
  cefiRoute: {
    provider: 'SEPA' | 'SWIFT' | 'ACH';
    fee: number;
    timeEstimate: string;
    compliance: boolean;
  };
  defiRoute: {
    protocol: 'Solana' | 'Jupiter';
    fee: number;
    timeEstimate: string;
    slippage: number;
  };
}

function selectOptimalRoute(
  amount: number,
  destination: string,
  userPreference: 'speed' | 'cost' | 'compliance'
): RouteOptions {
  // 1. Calculate CeFi route cost & time
  // 2. Calculate DeFi route cost & time
  // 3. Apply user preference weight
  // 4. Return optimal route with full transparency
}
```

---

## 4. System Architecture

### 4.1 Microservices Architecture

```
NeoBank Chain Backend
│
├── 🔐 auth-service          (Port 3001)
│   ├── JWT token management
│   ├── Biometric authentication
│   ├── KYC/AML verification (Jumio)
│   ├── 2FA (TOTP)
│   └── Session management (Redis)
│
├── 👤 user-service           (Port 3002)
│   ├── User profile management
│   ├── Account settings
│   ├── Notification preferences
│   └── Compliance records
│
├── 💳 wallet-service         (Port 3003)
│   ├── Multi-currency wallet management
│   ├── Fiat balance tracking (PostgreSQL)
│   ├── Crypto balance (Solana on-chain)
│   ├── Transaction history (aggregated)
│   └── Portfolio analytics
│
├── 💸 transfer-service       (Port 3004)
│   ├── Smart routing engine (CeFi vs DeFi)
│   ├── SEPA/SWIFT processing
│   ├── Solana P2P transfers
│   ├── Fee calculation
│   └── Transaction status tracking
│
├── 📈 defi-service           (Port 3005)
│   ├── Yield strategy management
│   ├── Staking operations (Jito)
│   ├── Lending operations (Solend)
│   ├── DEX operations (Jupiter)
│   └── Risk assessment
│
├── 💱 fiat-service           (Port 3006)
│   ├── Fiat on-ramp (MoonPay)
│   ├── Fiat off-ramp (MoonPay)
│   ├── Currency conversion
│   └── Banking partner APIs
│
└── 🔔 notification-service   (Port 3007)
    ├── Push notifications (Firebase)
    ├── Email notifications
    ├── SMS alerts
    └── In-app notifications
```

### 4.2 Infrastructure Architecture

```
AWS Infrastructure — Multi-Region

Region: EU-West-1 (Primary)          Region: US-East-1 (Secondary)
──────────────────────────           ──────────────────────────────
  ECS Fargate (containers)             ECS Fargate (containers)
  RDS PostgreSQL (Multi-AZ)            RDS PostgreSQL (Read replica)
  ElastiCache Redis                    ElastiCache Redis
  API Gateway                          API Gateway
         │                                    │
         └──────────── Route 53 ──────────────┘
                       (DNS Failover)
                           │
                    CloudFront CDN
                    (Global Edge)
                           │
                    Mobile Clients
```

---

## 5. Smart Contract Architecture

### 5.1 Contract Overview

```
Solana Programs (Smart Contracts)
Built with Rust + Anchor Framework

programs/
├── wallet_program/
│   ├── src/
│   │   ├── lib.rs              ← Program entry point
│   │   ├── instructions/
│   │   │   ├── create_wallet.rs
│   │   │   ├── deposit.rs
│   │   │   └── withdraw.rs
│   │   ├── state/
│   │   │   └── wallet.rs       ← Account state
│   │   └── errors.rs
│   └── Cargo.toml
│
├── transfer_program/
│   ├── src/
│   │   ├── lib.rs
│   │   ├── instructions/
│   │   │   ├── p2p_transfer.rs
│   │   │   ├── batch_transfer.rs
│   │   │   └── scheduled_transfer.rs
│   │   └── state/
│   │       └── transfer.rs
│   └── Cargo.toml
│
├── savings_program/
│   ├── src/
│   │   ├── lib.rs
│   │   ├── instructions/
│   │   │   ├── create_vault.rs
│   │   │   ├── deposit_yield.rs
│   │   │   └── claim_rewards.rs
│   │   └── state/
│   │       └── vault.rs
│   └── Cargo.toml
│
└── lending_program/
    ├── src/
    │   ├── lib.rs
    │   ├── instructions/
    │   │   ├── create_loan.rs
    │   │   ├── repay_loan.rs
    │   │   └── liquidate.rs
    │   └── state/
    │       └── loan.rs
    └── Cargo.toml
```

### 5.2 Wallet Program — Core Contract

```rust
// wallet_program/src/lib.rs
use anchor_lang::prelude::*;
use anchor_spl::token::{self, Token, TokenAccount, Transfer};

declare_id!("NEOBANK_WALLET_PROGRAM_ID");

#[program]
pub mod wallet_program {
    use super::*;

    /// Creates a new NeoBank Chain wallet for a user
    pub fn create_wallet(
        ctx: Context<CreateWallet>,
        bump: u8,
    ) -> Result<()> {
        let wallet = &mut ctx.accounts.wallet;
        wallet.owner = ctx.accounts.owner.key();
        wallet.bump = bump;
        wallet.is_active = true;
        wallet.created_at = Clock::get()?.unix_timestamp;
        wallet.total_transactions = 0;

        emit!(WalletCreated {
            owner: wallet.owner,
            created_at: wallet.created_at,
        });

        Ok(())
    }

    /// Executes a P2P transfer between two wallets
    pub fn transfer(
        ctx: Context<TransferFunds>,
        amount: u64,
        memo: String,
    ) -> Result<()> {
        require!(amount > 0, NeoError::InvalidAmount);
        require!(memo.len() <= 100, NeoError::MemoTooLong);
        require!(
            ctx.accounts.sender_token.amount >= amount,
            NeoError::InsufficientFunds
        );

        // Execute token transfer
        let transfer_instruction = Transfer {
            from: ctx.accounts.sender_token.to_account_info(),
            to: ctx.accounts.receiver_token.to_account_info(),
            authority: ctx.accounts.sender.to_account_info(),
        };

        token::transfer(
            CpiContext::new(
                ctx.accounts.token_program.to_account_info(),
                transfer_instruction,
            ),
            amount,
        )?;

        // Calculate and collect fee (0.1% — 0.5%)
        let fee = calculate_fee(amount);

        // Update transaction counters
        ctx.accounts.sender_wallet.total_transactions += 1;

        emit!(TransferExecuted {
            sender: ctx.accounts.sender.key(),
            receiver: ctx.accounts.receiver.key(),
            amount,
            fee,
            memo,
            timestamp: Clock::get()?.unix_timestamp,
        });

        Ok(())
    }
}

/// Wallet account state
#[account]
pub struct WalletAccount {
    pub owner: Pubkey,           // 32 bytes
    pub bump: u8,                // 1 byte
    pub is_active: bool,         // 1 byte
    pub created_at: i64,         // 8 bytes
    pub total_transactions: u64, // 8 bytes
}

impl WalletAccount {
    pub const LEN: usize = 8 + 32 + 1 + 1 + 8 + 8; // discriminator + fields
}

/// Custom error codes
#[error_code]
pub enum NeoError {
    #[msg("Transfer amount must be greater than zero")]
    InvalidAmount,
    #[msg("Insufficient funds for this transfer")]
    InsufficientFunds,
    #[msg("Memo cannot exceed 100 characters")]
    MemoTooLong,
    #[msg("Wallet is not active")]
    WalletInactive,
    #[msg("Unauthorized operation")]
    Unauthorized,
}

/// Fee calculation — transparent and on-chain
fn calculate_fee(amount: u64) -> u64 {
    // 0.1% fee — minimum 1 lamport
    let fee = amount / 1000;
    fee.max(1)
}

/// Events — emitted on-chain for full transparency
#[event]
pub struct WalletCreated {
    pub owner: Pubkey,
    pub created_at: i64,
}

#[event]
pub struct TransferExecuted {
    pub sender: Pubkey,
    pub receiver: Pubkey,
    pub amount: u64,
    pub fee: u64,
    pub memo: String,
    pub timestamp: i64,
}
```

### 5.3 Security Patterns

```rust
// Security best practices in every contract

// ✅ 1. Check-Effects-Interactions Pattern
pub fn secure_withdraw(ctx: Context<Withdraw>, amount: u64) -> Result<()> {
    // CHECK first — validate all conditions
    require!(amount > 0, NeoError::InvalidAmount);
    require!(
        ctx.accounts.vault.amount >= amount,
        NeoError::InsufficientFunds
    );
    require!(
        ctx.accounts.owner.key() == ctx.accounts.vault.owner,
        NeoError::Unauthorized
    );

    // EFFECTS — update state before external calls
    ctx.accounts.vault.amount -= amount;
    ctx.accounts.vault.last_withdrawal = Clock::get()?.unix_timestamp;

    // INTERACTIONS — external calls last
    token::transfer(/* ... */)?;

    Ok(())
}

// ✅ 2. Reentrancy protection via Anchor's automatic checks
// ✅ 3. Integer overflow protection (Rust built-in)
// ✅ 4. Owner verification on every sensitive instruction
// ✅ 5. PDA (Program Derived Address) for deterministic accounts
```

---

## 6. CeFi Integration Layer

### 6.1 Banking Integrations

```typescript
// CeFi Service Architecture

interface CeFiConfig {
  stripe: {
    apiKey: string;
    webhookSecret: string;
    supportedCurrencies: string[];
  };
  moonpay: {
    apiKey: string;
    secretKey: string;
    supportedCountries: string[];
  };
  sepa: {
    bankCode: string;
    iban: string;
    bic: string;
  };
}

// Fiat On-Ramp Flow
async function fiatToSolana(
  userAddress: string,
  fiatAmount: number,
  fiatCurrency: string,
  targetToken: 'USDC' | 'SOL'
): Promise<Transaction> {
  // 1. Verify user KYC status
  await verifyKYC(userAddress);

  // 2. Process fiat payment via MoonPay
  const fiatTx = await moonpay.createTransaction({
    baseCurrencyAmount: fiatAmount,
    baseCurrencyCode: fiatCurrency,
    currencyCode: targetToken,
    walletAddress: userAddress,
  });

  // 3. Wait for fiat confirmation
  await waitForFiatConfirmation(fiatTx.id);

  // 4. Mint/transfer tokens on Solana
  const solanaTx = await transferTokensToUser(
    userAddress,
    fiatTx.receivedCurrencyAmount,
    targetToken
  );

  return solanaTx;
}
```

### 6.2 KYC/AML Integration

```typescript
// Jumio KYC Integration
interface KYCResult {
  status: 'APPROVED' | 'REJECTED' | 'PENDING';
  userId: string;
  riskScore: number;
  countryCode: string;
  verifiedAt: Date;
}

async function performKYC(userId: string, documents: Document[]): Promise<KYCResult> {
  const jumioScan = await jumio.createScan({
    userReference: userId,
    reportingCriteria: 'NeoBank-Chain-KYC',
    workflowId: KYC_WORKFLOW_ID,
  });

  // Upload identity documents
  for (const doc of documents) {
    await jumio.uploadDocument(jumioScan.scanReference, doc);
  }

  // Initiate verification
  const result = await jumio.initiateVerification(jumioScan.scanReference);

  // Store compliance record on-chain (hashed — privacy preserved)
  await storeComplianceRecord(userId, hashKYCResult(result));

  return result;
}
```

---

## 7. DeFi Integration Layer

### 7.1 Jupiter DEX Integration

```typescript
// Jupiter — Best-price DEX aggregator
import { Jupiter, RouteInfo } from '@jup-ag/core';
import { Connection, PublicKey } from '@solana/web3.js';

async function getBestSwapRoute(
  inputMint: PublicKey,  // e.g., USDC
  outputMint: PublicKey, // e.g., SOL
  amount: number,
  slippageBps: number = 50 // 0.5% max slippage
): Promise<RouteInfo> {
  const jupiter = await Jupiter.load({
    connection: new Connection(SOLANA_RPC_URL),
    cluster: 'mainnet-beta',
    user: userPublicKey,
  });

  const routes = await jupiter.computeRoutes({
    inputMint,
    outputMint,
    amount,
    slippageBps,
    feeBps: 10, // NeoBank Chain 0.1% fee
  });

  // Return the best route (highest output, lowest fee)
  return routes.routesInfos[0];
}
```

### 7.2 Jito Liquid Staking

```typescript
// Jito — Liquid staking for yield generation
async function stakeForYield(
  userWallet: PublicKey,
  solAmount: number
): Promise<{
  jitoSOLReceived: number;
  currentAPY: number;
  estimatedYearlyEarnings: number;
}> {
  const jitoAPY = await jito.getCurrentAPY(); // ~7-8% APY

  const stakeResult = await jito.stake({
    wallet: userWallet,
    amount: solAmount,
    referral: NEOBANK_REFERRAL_KEY,
  });

  return {
    jitoSOLReceived: stakeResult.jitoSOLAmount,
    currentAPY: jitoAPY,
    estimatedYearlyEarnings: solAmount * jitoAPY,
  };
}
```

---

## 8. Security Architecture

### 8.1 Security Layers

```
Layer 1 — Network Security
├── AWS WAF (Web Application Firewall)
├── DDoS protection (AWS Shield)
├── TLS 1.3 for all communications
└── VPN for internal services

Layer 2 — Application Security
├── JWT with RS256 (asymmetric signing)
├── Rate limiting per user/IP
├── Input validation & sanitization
├── SQL injection prevention (ORM)
└── CORS policy enforcement

Layer 3 — Blockchain Security
├── Smart contract audits (Halborn/OtterSec)
├── Multi-signature treasury (3-of-5)
├── Time-locked admin functions
├── Emergency pause mechanism
└── JitoBAM MEV protection

Layer 4 — User Security
├── Biometric authentication
├── Hardware security module (HSM) for keys
├── Secure Enclave (iOS) / StrongBox (Android)
├── Anti-phishing measures
└── Real-time fraud detection (ML)
```

### 8.2 Key Management

```
Self-Custody Model:
┌─────────────────────────────────────────────────┐
│              USER'S DEVICE                       │
│                                                  │
│  Private Key → Encrypted in Secure Enclave      │
│  Never leaves the device                         │
│  NeoBank Chain NEVER has access                  │
└─────────────────────────────────────────────────┘

Custodial Model (optional):
┌─────────────────────────────────────────────────┐
│              NEOBANK CHAIN HSM                   │
│                                                  │
│  Private Keys → AWS CloudHSM                    │
│  FIPS 140-2 Level 3 certified                   │
│  Assets insured up to $250,000                  │
│  5% hot wallet / 95% cold storage               │
└─────────────────────────────────────────────────┘
```

---

## 9. Data Architecture

### 9.1 Database Schema

```sql
-- Core tables (PostgreSQL)

-- Users table
CREATE TABLE users (
    id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    email           VARCHAR(255) UNIQUE NOT NULL,
    phone           VARCHAR(20) UNIQUE,
    kyc_status      VARCHAR(20) DEFAULT 'PENDING',
    kyc_verified_at TIMESTAMP,
    risk_score      INTEGER DEFAULT 0,
    country_code    CHAR(2) NOT NULL,
    created_at      TIMESTAMP DEFAULT NOW(),
    updated_at      TIMESTAMP DEFAULT NOW()
);

-- Wallets table
CREATE TABLE wallets (
    id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    user_id         UUID REFERENCES users(id),
    solana_address  VARCHAR(44) UNIQUE,  -- Solana public key
    wallet_type     VARCHAR(20),         -- 'custodial' | 'self-custody'
    is_active       BOOLEAN DEFAULT TRUE,
    created_at      TIMESTAMP DEFAULT NOW()
);

-- Transactions table
CREATE TABLE transactions (
    id              UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    sender_id       UUID REFERENCES users(id),
    receiver_id     UUID REFERENCES users(id),
    amount          DECIMAL(20, 8) NOT NULL,
    currency        VARCHAR(10) NOT NULL,
    tx_type         VARCHAR(20) NOT NULL,  -- 'cefi' | 'defi' | 'bridge'
    status          VARCHAR(20) DEFAULT 'PENDING',
    solana_tx_hash  VARCHAR(88),           -- On-chain reference
    fee_amount      DECIMAL(20, 8),
    created_at      TIMESTAMP DEFAULT NOW(),
    completed_at    TIMESTAMP
);

-- Indexes for performance
CREATE INDEX idx_transactions_sender ON transactions(sender_id);
CREATE INDEX idx_transactions_receiver ON transactions(receiver_id);
CREATE INDEX idx_transactions_created ON transactions(created_at DESC);
CREATE INDEX idx_wallets_user ON wallets(user_id);
```

---

## 10. API Architecture

### 10.1 REST API Design

```
Base URL: https://api.neobankchain.io/v1

Authentication:
  Authorization: Bearer <JWT_TOKEN>

Endpoints:

AUTH
POST   /auth/register          Register new user
POST   /auth/login             Login with email/password
POST   /auth/biometric         Biometric authentication
POST   /auth/kyc/initiate      Start KYC verification
GET    /auth/kyc/status        Check KYC status

WALLET
GET    /wallet                 Get wallet overview
GET    /wallet/balance         Get all balances (fiat + crypto)
GET    /wallet/transactions    Get transaction history
POST   /wallet/create          Create new wallet

TRANSFERS
POST   /transfer/send          Send money (CeFi or DeFi route)
GET    /transfer/estimate      Get transfer fee estimate
GET    /transfer/routes        Get available routes
GET    /transfer/:id           Get transfer status

DEFI
GET    /defi/yields            Get available yield products
POST   /defi/stake             Stake SOL with Jito
POST   /defi/unstake           Unstake SOL
GET    /defi/positions         Get active DeFi positions

FIAT
POST   /fiat/onramp            Buy crypto with fiat
POST   /fiat/offramp           Sell crypto for fiat
GET    /fiat/rates             Get exchange rates
```

### 10.2 WebSocket Events

```typescript
// Real-time events via WebSocket
interface WebSocketEvents {
  // Incoming events (server → client)
  'balance.updated': {
    currency: string;
    newBalance: number;
    change: number;
  };
  'transfer.confirmed': {
    transferId: string;
    txHash: string;
    confirmationTime: number; // milliseconds
  };
  'yield.earned': {
    protocol: string;
    amount: number;
    currency: string;
  };
  'price.update': {
    symbol: string;
    price: number;
    change24h: number;
  };
}
```

---

## 11. Mobile Architecture

### 11.1 React Native Structure

```
mobile/
├── src/
│   ├── screens/
│   │   ├── Auth/
│   │   │   ├── LoginScreen.tsx
│   │   │   ├── RegisterScreen.tsx
│   │   │   └── KYCScreen.tsx
│   │   ├── Dashboard/
│   │   │   ├── DashboardScreen.tsx
│   │   │   ├── BalanceCard.tsx
│   │   │   └── QuickActions.tsx
│   │   ├── Transfer/
│   │   │   ├── SendScreen.tsx
│   │   │   ├── ReceiveScreen.tsx
│   │   │   └── RouteSelector.tsx
│   │   └── DeFi/
│   │       ├── YieldScreen.tsx
│   │       ├── StakingScreen.tsx
│   │       └── PortfolioScreen.tsx
│   │
│   ├── components/
│   │   ├── WalletCard.tsx
│   │   ├── TransactionItem.tsx
│   │   ├── CurrencySelector.tsx
│   │   └── BiometricPrompt.tsx
│   │
│   ├── services/
│   │   ├── api.service.ts      ← HTTP client
│   │   ├── solana.service.ts   ← Blockchain interactions
│   │   ├── wallet.service.ts   ← Wallet management
│   │   └── biometric.service.ts ← Biometric auth
│   │
│   ├── store/
│   │   ├── auth.store.ts       ← Zustand state
│   │   ├── wallet.store.ts
│   │   └── defi.store.ts
│   │
│   └── utils/
│       ├── formatCurrency.ts
│       ├── validateAddress.ts
│       └── cryptoHelpers.ts
│
├── android/
├── ios/
└── package.json
```

---

## 12. Performance & Scalability

### 12.1 Performance Targets

| Metric | Target | How |
|---|---|---|
| API Response Time | < 200ms (p95) | Redis cache + optimized queries |
| App Load Time | < 2s | Code splitting + lazy loading |
| Transfer Confirmation | < 1s | Solana Alpenglow (150ms finality) |
| Concurrent Users | 100,000+ | Horizontal scaling (ECS) |
| Uptime | 99.99% | Multi-region + failover |
| Transaction TPS | 10,000+ | Solana's 65,000 TPS capacity |

### 12.2 Caching Strategy

```
Redis Cache Layers:

L1 — User Sessions      (TTL: 24h)
L2 — Price Feeds        (TTL: 10s)  ← Pyth oracle data
L3 — Exchange Rates     (TTL: 60s)
L4 — DeFi APY Rates     (TTL: 5min)
L5 — User Balances      (TTL: 30s)  ← Invalidated on tx
```

---

## 13. Code Standards & Patterns

### 13.1 TypeScript Standards

```typescript
// ✅ Always use strict TypeScript
// tsconfig.json
{
  "compilerOptions": {
    "strict": true,
    "noImplicitAny": true,
    "strictNullChecks": true,
    "noUnusedVariables": true,
    "noUnusedParameters": true
  }
}

// ✅ Always handle errors explicitly
async function transferFunds(params: TransferParams): Promise<Result<Transaction, NeoError>> {
  try {
    const tx = await executeTransfer(params);
    return { success: true, data: tx };
  } catch (error) {
    logger.error('Transfer failed', { error, params });
    return { success: false, error: mapError(error) };
  }
}

// ✅ Use enums for constants
enum TransactionStatus {
  PENDING = 'PENDING',
  PROCESSING = 'PROCESSING',
  CONFIRMED = 'CONFIRMED',
  FAILED = 'FAILED',
}

// ✅ Validate all inputs
function validateTransferAmount(amount: number): void {
  if (!Number.isFinite(amount)) throw new NeoError('INVALID_AMOUNT');
  if (amount <= 0) throw new NeoError('AMOUNT_TOO_LOW');
  if (amount > MAX_TRANSFER_LIMIT) throw new NeoError('AMOUNT_TOO_HIGH');
}
```

### 13.2 Testing Standards

```typescript
// Every function must have tests
// Target: >90% code coverage

describe('Transfer Service', () => {
  it('should select DeFi route for international transfers', async () => {
    const route = await routeSelector.getBestRoute({
      amount: 100,
      currency: 'USD',
      destination: 'JP',
      preference: 'speed',
    });

    expect(route.type).toBe('DEFI');
    expect(route.estimatedTime).toBeLessThan(2000); // < 2 seconds
    expect(route.fee).toBeLessThan(0.5); // < 0.5%
  });

  it('should reject transfers with insufficient balance', async () => {
    await expect(
      transferService.send({ amount: 1000000, userBalance: 100 })
    ).rejects.toThrow('InsufficientFunds');
  });
});
```

---

## 📬 Technical Contact

- **GitHub:** [github.com/machrouh35/NeoBank-Chain](https://github.com/machrouh35/NeoBank-Chain)
- **Email:** contact@neobankchain.io
- **Documentation Version:** 1.0 — April 2026

---

<div align="center">

**NeoBank Chain** — *Your bank, your rules, on blockchain* 🚀

*Built with Rust • TypeScript • React Native • Solana*
*Security-first • Compliance-ready • Institutional-grade*

</div>
