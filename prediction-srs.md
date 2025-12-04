# PREDICTION MARKET - SRS

> Tài liệu mô tả sản phẩm cho team Business, Marketing, Operations, Product

---

## 1. PRODUCT OVERVIEW

### Mô Tả Ngắn Gọn
**Trading Terminal** chuyên biệt cho **Crypto Premarket** - giúp trader giao dịch các token chưa ra mắt (pre-launch tokens) một cách **nhanh chóng, chuyên nghiệp và hiệu quả** với trải nghiệm **gasless**.

### Crypto Premarket là gì?

```
┌─────────────────────────────────────────────────────────────────┐
│                    CRYPTO PREMARKET                             │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  Prediction market cho các token CHƯA được list:                │
│                                                                 │
│  • Token từ các dự án sắp TGE (Token Generation Event)          │
│  • Airdrop tokens chưa claim được                               │
│  • Points/Miles có thể convert thành token                      │
│                                                                 │
│  Ví dụ:                                                         │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ "GRASS token price at TGE"                              │   │
│  │  YES (>$2): $0.65  |  NO (<$2): $0.35                   │   │
│  │                                                         │   │
│  │ "LayerZero airdrop value"                               │   │
│  │  YES (>$500): $0.42  |  NO (<$500): $0.58               │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### Vấn Đề Hiện Tại

| Vấn đề | Ảnh hưởng đến trader |
|--------|----------------------|
| UI không tối ưu cho trading | Khó theo dõi nhiều markets cùng lúc |
| Không có TP/SL orders | Không thể auto take profit hay stop loss |
| Portfolio tracking yếu | Khó phân tích P&L, không có analytics |
| Khó track smart money | Không biết big players đang bet gì, volume đến từ đâu |
| Phải trả gas mỗi lần deposit | Tốn phí, trải nghiệm không mượt |

### Giải Pháp Của Chúng Ta

```
┌─────────────────────────────────────────────────────────────────┐
│           TRADING TERMINAL FOR CRYPTO PREMARKET                 │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  🎯 TỐI ƯU CHO TRADER:                                          │
│                                                                 │
│  • Professional trading interface                               │
│  • Multi-market monitoring & watchlists                         │
│  • TP/SL orders (coming soon)                                   │
│  • Real-time P&L tracking & analytics                           │
│  • Smart money tracking & whale alerts                          │
│                                                                 │
│  ⚡ GASLESS EXPERIENCE:                                         │
│                                                                 │
│  • Gasless deposit - không tốn gas khi nạp tiền                 │
│  • Deposit từ bất kỳ chain nào                                  │
│  • Tự động bridge, user không cần làm gì                        │
│  • Fast order execution                                         │
│  • Direct settlement về wallet                                  │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### Lưu Ý Quan Trọng

```
┌─────────────────────────────────────────────────────────────────┐
│ 📌 PLATFORM LÀM GÌ VÀ KHÔNG LÀM GÌ                              │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│ ✅ CHÚNG TA LÀM:                                                │
│    • Hiển thị Crypto Premarket từ Polymarket                    │
│    • Cung cấp trading terminal chuyên nghiệp                    │
│    • Forward orders sang Polymarket execution                   │
│    • Gasless deposit cho seamless experience                    │
│                                                                 │
│ ❌ CHÚNG TA KHÔNG LÀM:                                          │
│    • KHÔNG làm Politics, Sports, hay Events markets             │
│    • KHÔNG tìm best price giữa các platforms                    │
│    • KHÔNG tự tạo markets hay quyết định resolution             │
│                                                                 │
│ 🎯 FOCUS: Crypto Premarket only                                 │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

## 2. SYSTEM ARCHITECTURE

### Overview

```
┌─────────────────────────────────────────────────────────────────┐
│                    TRADING TERMINAL ARCHITECTURE                │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   USER                                                          │
│   ┌─────────────┐                                               │
│   │  Connect    │  Email, Google, hoặc external wallet          │
│   │  Wallet     │  (Privy embedded wallet)                      │
│   └──────┬──────┘                                               │
│          │                                                      │
│          ▼                                                      │
│   ┌─────────────┐     ┌──────────────────────────────────┐      │
│   │  Deposit    │────►│      GASLESS SMART DEPOSIT       │      │
│   │  (Any Chain)│     │  • Receive funds on any chain    │      │
│   └─────────────┘     │  • NO GAS required from user     │      │
│                       │  • Auto-bridge to Polygon        │      │
│                       │  • Credit USDT to user           │      │
│                       └──────────────────────────────────┘      │
│          │                                                      │
│          ▼                                                      │
│   ┌─────────────────────────────────────────────────────────┐   │
│   │                   TRADING TERMINAL                      │   │
│   │                                                         │   │
│   │  ┌─────────┐  ┌─────────┐  ┌─────────┐  ┌─────────┐     │   │
│   │  │Premarket│  │ Order   │  │Portfolio│  │ Smart   │     │   │
│   │  │ Browser │  │ Panel   │  │ Manager │  │ Money   │     │   │
│   │  └─────────┘  └─────────┘  └─────────┘  └─────────┘     │   │
│   │                                                         │   │
│   └─────────────────────────┬───────────────────────────────┘   │
│                             │                                   │
│                             ▼                                   │
│   ┌─────────────────────────────────────────────────────────┐   │
│   │                    ORDER EXECUTION                      │   │
│   │                                                         │   │
│   │  Smart Contract ──► Relayer ──► Polymarket ──► Result   │   │
│   │                                                         │   │
│   └─────────────────────────────────────────────────────────┘   │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### Components

| Component | Mô tả |
|-----------|-------|
| **Privy Wallet** | Embedded wallet, login bằng email/Google/external wallet |
| **Gasless Smart Deposit** | Nhận crypto từ mọi chain, user KHÔNG cần trả gas |
| **Trading Terminal** | Interface chính cho trader, focus Crypto Premarket |
| **Order Execution** | Smart contract + Relayer forward orders sang Polymarket |

---

## 3. USER FLOWS

### 3.1 Gasless Deposit Flow

**Điểm khác biệt: User KHÔNG cần trả gas khi deposit**

```
[1] User chọn "Deposit" trong app
    │
    ▼
[2] System hiển thị deposit addresses cho các chains
    ┌─────────────────────────────────────────┐
    │ DEPOSIT                                 │
    │                                         │
    │ Send USDT/USDC to any address below:    │
    │                                         │
    │ Polygon:  0xAbc...123                   │
    │ Arbitrum: 0xDef...456                   │
    │ Base:     0xGhi...789                   │
    │ BSC:      0xJkl...012                   │
    │                                         │
    │ ⚡ GASLESS - You don't pay any gas      │
    │ ⚡ Auto-converted to USDT               │
    │ ⚡ Ready to trade in ~2-5 mins          │
    └─────────────────────────────────────────┘
    │
    ▼
[3] User gửi crypto từ wallet/CEX của họ
    → User chỉ cần gửi token, KHÔNG cần giữ native token cho gas
    │
    ▼
[4] Gasless Smart Deposit xử lý:
    → Detect incoming funds
    → System pays gas (user không trả)
    → Auto-bridge to Polygon (nếu cần)
    → Convert to USDT (nếu cần)
    → Credit to user balance
    │
    ▼
[5] User thấy balance trong Trading Terminal
    → Ready to trade!

⏱️ Processing time: 2-5 minutes
💰 Gas cost for user: $0
```

**Ví dụ:**
```
Trader muốn deposit $1,000 USDT từ Arbitrum

Step 1: Copy Arbitrum deposit address
Step 2: Send 1,000 USDT từ personal wallet hoặc CEX
        → User KHÔNG cần giữ ETH cho gas
        → Chỉ cần có USDT là đủ
Step 3: Gasless Smart Deposit nhận và bridge sang Polygon
        → System trả gas, không phải user
Step 4: Balance updated: +1,000 USDT

User pays: $0 gas
Deposit Fee: $0 (0%)
```

**So sánh với deposit thông thường:**

| Aspect | Deposit thường | Gasless Deposit |
|--------|----------------|-----------------|
| User cần native token (ETH/BNB) | ✅ Cần | ❌ Không cần |
| User trả gas | ✅ ~$0.5-5 | ❌ $0 |
| Số bước | 2-3 bước | 1 bước |
| Trải nghiệm | Phức tạp | Đơn giản |

**Supported tokens:**
| Token | Chains |
|-------|--------|
| USDT | Polygon, Arbitrum, Base, BSC |
| USDC | Polygon, Arbitrum, Base, BSC |

---

### 3.2 Buy Order Flow

**Quy trình:**
```
[1] Chọn Premarket trong Terminal
    Ví dụ: "GRASS token > $2 at TGE"
    │
    ▼
[2] Chọn Outcome: YES hoặc NO
    │
    ▼
[3] Nhập Amount
    │
    ▼
[4] Review Order
    ┌─────────────────────────────────────────┐
    │ BUY ORDER                               │
    │                                         │
    │ Market:  GRASS > $2 at TGE              │
    │ Side:    YES                            │
    │ Price:   $0.65                          │
    │ Amount:  $100                           │
    │ Shares:  ~153                           │
    │ Fee:     $1 (1%)                        │
    │ Total:   $101                           │
    │                                         │
    │ [Cancel]              [Confirm Order]   │
    └─────────────────────────────────────────┘
    │
    ▼
[5] Confirm & Sign transaction
    │
    ▼
[6] Order executed on Polymarket
    │
    ▼
[7] Position appears in Portfolio
    → 153 YES shares @ $0.65

⏱️ Execution time: 30 seconds - 2 minutes
```

**Order outcomes:**

| Kết quả | Xử lý |
|---------|-------|
| ✅ Filled | Position created, refund unused (nếu có) |
| ❌ Failed | Full refund to wallet |
| ⏰ Expired | Full refund to wallet |

---

### 3.3 Sell Order Flow

**Quy trình:**
```
[1] Vào Portfolio, chọn position
    │
    ▼
[2] Click "Sell" và nhập quantity
    │
    ▼
[3] Review Order
    ┌─────────────────────────────────────────┐
    │ SELL ORDER                              │
    │                                         │
    │ Market:  GRASS > $2 at TGE              │
    │ Shares:  100 (of 153)                   │
    │ Price:   $0.78                          │
    │ Gross:   $78.00                         │
    │ Fee:     $0.78 (1%)                     │
    │ Net:     $77.22                         │
    │                                         │
    │ [Cancel]              [Confirm Sell]    │
    └─────────────────────────────────────────┘
    │
    ▼
[4] Confirm & Sign
    │
    ▼
[5] Order executed
    │
    ▼
[6] USDT credited to wallet (direct)
    → +$77.22 USDT

⏱️ Execution time: 30 seconds - 2 minutes
```

---

### 3.4 Settlement Flow (Market Resolves)

**Khi market kết thúc và có kết quả:**
```
[1] Event xảy ra
    Ví dụ: GRASS token TGE, giá mở = $2.50
    │
    ▼
[2] Polymarket công bố resolution
    Result: YES ✓ (vì $2.50 > $2)
    │
    ▼
[3] System tính payout cho winners
    ┌─────────────────────────────────────────┐
    │ Position:    150 YES shares             │
    │ Cost basis:  $97.50                     │
    │ Payout:      $150.00                    │
    │ Profit:      +$52.50                    │
    │ Fee:         $0 (no settlement fee)     │
    │ Claimable:   $150.00                    │
    └─────────────────────────────────────────┘
    │
    ▼
[4] User thấy "Claim" button trong Portfolio
    │
    ▼
[5] User click Claim
    │
    ▼
[6] USDT sent to wallet (direct)
    → +$150.00 USDT

⏱️ Settlement: 1-24 hours after TGE/event
⏱️ Claim: Instant
```

**Losing position:**
```
Market resolves: NO (GRASS = $1.80, dưới $2)
User holds: YES shares
Result: Shares worth $0
Status: SETTLED_LOST
```

---

## 4. ORDER STATUS

### Buy Order Status

| Status | Meaning |
|--------|---------|
| `PENDING` | Order submitted, processing |
| `FILLED` | Successfully executed |
| `FAILED` | Execution failed, refunding |
| `REFUNDED` | Funds returned to wallet |
| `EXPIRED` | Order expired (>5 min) |

### Sell Order Status

| Status | Meaning |
|--------|---------|
| `PENDING` | Sell order processing |
| `FILLED` | Sold, USDT in wallet |
| `FAILED` | Failed, shares unlocked |

### Position Status

| Status | Meaning |
|--------|---------|
| `ACTIVE` | Holding, can sell anytime |
| `CLAIMABLE` | Won, click Claim to receive USDT |
| `CLAIMED` | USDT already received |
| `SETTLED_LOST` | Lost, shares worth $0 |

---

## 5. PROCESSING TIMES

| Action | Time | Notes |
|--------|------|-------|
| Gasless Deposit | 2-5 minutes | Auto-bridge included, no gas for user |
| Buy Order | 30s - 2 min | |
| Sell Order | 30s - 2 min | USDT direct to wallet |
| Settlement | 1-24 hours | After TGE or event |
| Claim | Instant | User pays gas |
| Refund | 5-30 minutes | After admin review |

---

## 6. FEE STRUCTURE

### Fee Overview

```
┌─────────────────────────────────────────────────────────────────┐
│                        FEE STRUCTURE                            │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│   Fee Type                Rate            Notes                 │
│   ───────────────────────────────────────────────────────────   │
│   Deposit Fee             0%              Free + Gasless        │
│   Trading Fee             1%              Per order (buy/sell)  │
│   Settlement Fee          0%              Free                  │
│   Gas Fee (deposit)       0%              System pays           │
│   Gas Fee (trade/claim)   User pays       Network dependent     │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### Fee Calculation Examples

**Buy Order:**
```
User mua $100 shares

Amount:      $100
Trading Fee: $1 (1%)
Total:       $101
```

**Sell Order:**
```
User bán shares, nhận $78 gross

Gross:       $78
Trading Fee: $0.78 (1%)
Net:         $77.22
```

---

## 7. SUPPORTED MARKETS

### Market Focus: Crypto Premarket Only

```
┌─────────────────────────────────────────────────────────────────┐
│                    CRYPTO PREMARKET CATEGORIES                  │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  📈 TOKEN TGE PREDICTIONS                                       │
│     • "GRASS > $2 at TGE"                                       │
│     • "EIGEN > $5 at listing"                                   │
│     • "ZRO opening price > $4"                                  │
│                                                                 │
│  🎁 AIRDROP VALUE PREDICTIONS                                   │
│     • "LayerZero airdrop > $500"                                │
│     • "zkSync airdrop > $1000"                                  │
│     • "Starknet allocation > 500 tokens"                        │
│                                                                 │
│  🎯 POINTS/MILES CONVERSION                                     │
│     • "Blast points worth > $0.001 each"                        │
│     • "EigenLayer points conversion rate"                       │
│                                                                 │
│  ❌ NOT INCLUDED:                                               │
│     • Politics (elections, policies)                            │
│     • Sports (game outcomes)                                    │
│     • Weather, Economics                                        │
│     • General events                                            │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

### Source Platform

| Platform | Status | Focus |
|----------|--------|-------|
| **Polymarket** | ✅ Live | Crypto Premarket markets only |

---

## 8. ERROR HANDLING

### Order Failure Scenarios

**Scenario 1: Insufficient Liquidity**
```
User places $100K buy order
→ Polymarket only has $50K available
→ Order status: FAILED
→ Action: Full refund to wallet
→ Notification: "Order failed - Insufficient liquidity"
```

**Scenario 2: Price Slippage**
```
User sets min sell price: $0.68
→ Actual price at execution: $0.66
→ Order status: FAILED (protects user)
→ Action: Shares unlocked, can retry
```

**Scenario 3: Platform Downtime**
```
Polymarket API unavailable
→ System retries for 10 minutes
→ If still failing: Order marked FAILED
→ Action: Full refund after admin review
```

### User Notifications

| Event | In-App | Push | Email |
|-------|--------|------|-------|
| Deposit received | ✅ | ✅ | ❌ |
| Order filled | ✅ | ✅ | ❌ |
| Order failed | ✅ | ✅ | ✅ |
| Refund processed | ✅ | ✅ | ✅ |
| Position claimable | ✅ | ✅ | ✅ |
| Position settled (lost) | ✅ | ✅ | ❌ |

---

## 9. PORTFOLIO INTERFACE

### Sample Portfolio View

```
┌─────────────────────────────────────────────────────────────────┐
│ PORTFOLIO                                           0x1234...56 │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│ 💰 BALANCE                                                      │
│ ┌─────────────────────────────────────────────────────────────┐ │
│ │                                                             │ │
│ │   1,250.00 USDT                        [Deposit]  [Send]    │ │
│ │                                                             │ │
│ └─────────────────────────────────────────────────────────────┘ │
│                                                                 │
│ 🎉 CLAIMABLE                                                    │
│ ┌─────────────────────────────────────────────────────────────┐ │
│ │                                                             │ │
│ │  "EIGEN > $5 at TGE" - WON YES                              │ │
│ │  Payout: $150.00 | Fee: $0 | Net: $150.00                   │ │
│ │                                           [Claim $150.00]   │ │
│ │                                                             │ │
│ └─────────────────────────────────────────────────────────────┘ │
│                                                                 │
│ 📈 ACTIVE POSITIONS (2)                      Total: $149.60     │
│ ┌─────────────────────────────────────────────────────────────┐ │
│ │                                                             │ │
│ │  GRASS > $2 at TGE                                  ACTIVE  │ │
│ │  150 YES @ $0.65 → $0.78 (+20%)                             │ │
│ │  Value: $117.00 | Cost: $97.50 | P&L: +$19.50               │ │
│ │                                          [Sell] [Details]   │ │
│ │                                                             │ │
│ ├─────────────────────────────────────────────────────────────┤ │
│ │                                                             │ │
│ │  LayerZero airdrop > $500                           ACTIVE  │ │
│ │  80 NO @ $0.45 → $0.52 (+15.6%)                             │ │
│ │  Value: $41.60 | Cost: $36.00 | P&L: +$5.60                 │ │
│ │                                          [Sell] [Details]   │ │
│ │                                                             │ │
│ └─────────────────────────────────────────────────────────────┘ │
│                                                                 │
│ 📜 HISTORY                                                      │
│ ┌─────────────────────────────────────────────────────────────┐ │
│ │ ✅ Claimed "ZRO > $4" +$85.50                     2 hrs ago │ │
│ │ ❌ SETTLED_LOST "STRK airdrop > $2000"           1 day ago │ │
│ │ 💰 Deposit +500 USDT (Gasless from Arbitrum)      3 hrs ago │ │
│ └─────────────────────────────────────────────────────────────┘ │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

## 10. RISK & USER PROTECTION

### Potential Risks

| Risk | Impact | Mitigation |
|------|--------|------------|
| Polymarket downtime | Cannot execute orders | Queue & retry, refund if prolonged |
| Price slippage | Worse execution than expected | maxPrice/minPrice protection |
| Bridge failure | Deposit delayed | Multiple bridge providers |
| TGE delay | Market resolution delayed | Follow Polymarket's timeline |

### User Protections

| Protection | How It Works |
|------------|--------------|
| **Slippage Protection** | User sets max buy price / min sell price |
| **Order Expiry** | Orders auto-cancel after 5 minutes |
| **Direct Settlement** | Funds go straight to wallet, no lock-up |
| **Reviewed Refunds** | Failed orders manually verified before refund |
| **Gasless Deposit** | No risk of failed deposit due to insufficient gas |

---

## 11. DISPUTE RESOLUTION

### Resolution Process

```
User disputes result (within 24 hours)
         │
         ▼
Support team reviews (48h SLA)
         │
         ├── Polymarket resolution correct → Dispute rejected
         │
         ├── Polymarket made error → Escalate to Polymarket
         │
         └── Our system error → Compensate user
         │
         ▼
Result communicated to user
```

**Note:** We follow Polymarket's resolution. We do not independently decide market outcomes.

---

## SUMMARY

### What We Offer

| Feature | Description |
|---------|-------------|
| **Crypto Premarket Terminal** | Professional interface for pre-launch token trading |
| **Gasless Deposit** | Deposit without paying gas, from any chain |
| **Multi-market View** | Monitor multiple premarket opportunities |
| **Portfolio Analytics** | Real-time P&L tracking, performance analysis |
| **Smart Money Tracking** | Track whale movements, big player activities |
| **Fast Execution** | Orders forwarded to Polymarket instantly |
| **Direct Settlement** | Winnings go straight to wallet |

### Market Focus

| Category | Examples |
|----------|----------|
| **Token TGE** | GRASS, EIGEN, ZRO price at launch |
| **Airdrop Value** | LayerZero, zkSync, Starknet airdrops |
| **Points Conversion** | Blast points, EigenLayer points |
| ❌ **Not included** | Politics, Sports, Weather, General events |

### Fee Structure

| Fee Type | Rate |
|----------|------|
| Deposit Fee | 0% + Gasless |
| **Trading Fee** | **1%** |
| Settlement Fee | 0% |

### Fund Flow

```
┌─────────────────────────────────────────────────────────────┐
│  Action         │  Flow                                     │
├─────────────────────────────────────────────────────────────┤
│  Deposit        │  Any Chain → Gasless Bridge → Balance     │
│  Buy            │  Balance → Lock → Position                │
│  Buy (refund)   │  → Direct to Wallet                       │
│  Sell           │  Position → Direct to Wallet              │
│  Win            │  → Claimable → Claim → Wallet             │
│  Lose           │  Position value = $0                      │
└─────────────────────────────────────────────────────────────┘
```

---

**Document Version:** 1.0  
**Last Updated:** December 2025  
**Product:** Trading Terminal for Crypto Premarket  
**Source Platform:** Polymarket (Crypto Premarket markets)  
**Trading Fee:** 1%  
**Deposit:** Gasless
