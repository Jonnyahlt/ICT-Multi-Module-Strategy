# ICT Session Engine [Silver Bullet] - Advanced Indicator

## Overview
Professional ICT Silver Bullet implementation with multi-timeframe adaptive settings, HTF macro liquidity overlay, IFVG detection, and complete visual toolkit for institutional-style trading on NQ, ES, and major indices.

## Key Features

### 🎯 HTF Macro Liquidity Overlay
- **Yesterday's Daily H/L**: Major liquidity pools (thick solid lines, width 2)
- **4H Swing Levels**: Secondary macro reference (dashed, width 1)
- **Text Labels**: ATR-offset text above/below lines (no boxes)
- **Auto-Fade**: Grays out when swept
- **Zero Algorithm Impact**: Purely visual - doesn't affect signals

### 💧 Current TF Liquidity (BSL/SSL)
- **Smart Filtering**: Bar spacing + size threshold controls
- **Sensitivity Control**: 0.1 (many) → 1.0 (major only)
- **REQ Detection**: Relative Equal Highs/Lows within 2 handles
- **Clean Text**: ATR-offset labels (0.15 ATR) above/below lines
- **Default**: 8 bars spacing, 0.25 sensitivity (balanced)

### ⚙️ TF-Adaptive Settings
**6 core settings auto-scale across all timeframes (1m → Daily):**
- FVG Max Age: Base×10 (1m) → Base×0.5 (Daily)
- FVG Min Size: Base×2.0 (1m) → Base×0.5 (1H+) - **NEW AUTO-SCALING**
- OB Max Age: Same intelligent scaling
- Premium/Discount Swing: Base×0.5 (1m) → Base×2.5 (Daily)
- Equal H/L Lookback: 2 bars (1m) → 6 bars (Daily)
- Liquidity Threshold: 1.0% (1m) → 0.25% (Daily)

### 📦 Advanced FVG Management + IFVG (NEW)
- **First FVG**: 70% transparency, solid border, "#1" label (most important)
- **Other FVGs**: 85% transparency, dashed border
- **IFVG (Inverse FVG)**: FVG turns GRAY when filled = premium mitigation zone
- **ICT Concept**: Filled FVG becomes high-priority entry area
- **50% Midline**: Precision entry reference (dashed line at midpoint)
- **TF-Adaptive Sizing**: Single override value works across all TFs (e.g., 0.5 = perfect 5m/15m, auto-adjusts 1m/1H)
- Dynamic age-based invalidation

### 📦 Order Block Detection
- **ICT-Compliant**: Last opposing candle before engulfing
- **Visual Hierarchy**: Yellow (fresh) → Olive (breaker) → Gray (mitigated)
- **Relaxed Logic**: Balanced detection (not too many, not too few)
- **Optional Boxes**: Toggle for cleaner charts

### 📊 Session-Based Structure
- **Asia** (20:00-00:00 ET): Range building
- **London** (02:00-05:00 ET): Setup phase
- **NY AM** (09:30-11:00 ET): Primary killzone
- **NY PM** (13:30-16:00 ET): Secondary killzone

### 🎯 Silver Bullet Windows
- **London SB**: 03:00-04:00 ET
- **NY AM SB**: 10:00-11:00 ET (highest probability)
- **NY PM SB**: 14:00-15:00 ET

### 💧 Dual Liquidity Sweep Detection
- **Inter-Session**: London sweeps Asia, NY sweeps London
- **Intra-Session**: Session sweeps its own H/L
- Dashboard shows type: "(Prev)" or "(Intra)"

### 📈 HTF Bias Alignment
- Daily 50 EMA + Weekly 20 EMA + Monthly 12 EMA
- Dashboard shows ⭐ when all aligned
- Filter for highest probability setups

### 📱 Real-Time Dashboard
- Active session and SB window
- HTF alignment status
- Liquidity sweep type
- Premium/Discount zone
- Setup checklist (HTF → Liq → MSS → FVG)

## Entry Requirements

**Long Setup:**
✓ HTF Bias Bullish | ✓ SSL Swept | ✓ MSS Bullish | ✓ Discount Zone | ✓ FVG Retraced | ✓ SB Window

**Short Setup:**
✓ HTF Bias Bearish | ✓ BSL Swept | ✓ MSS Bearish | ✓ Premium Zone | ✓ FVG Retraced | ✓ SB Window

## Recommended Settings
- **Symbol**: NQ1!, ES1!, major indices
- **Timeframe**: 5m (scalping) or 15m (swing) - works 1m to Daily
- **Sessions**: London SB + NY AM SB (highest probability)
- **FVG Min Size Override**: 0.5 (auto-scales: 1.0 on 1m, 0.5 on 5m/15m, 0.25 on 1H+)
- **BSL/SSL Sensitivity**: 0.25 (balanced - shows important levels without clutter)
- **BSL/SSL Spacing**: 8 bars (default - adjust 3-20 for more/fewer levels)
- **Show IFVG**: ON (gray filled FVGs = premium entries)
- **HTF Macro Liquidity**: ON (Daily/4H visual context)
- **Dynamic Settings**: Use Base values (auto-scales per TF)

## Visual Hierarchy
1. **Yesterday's Daily H/L** - Thick solid width 2 (most important)
2. **4H Swing Levels** - Dashed width 1 (secondary macro)
3. **IFVG (Gray FVG)** - Filled FVG = mitigation zone (premium entries)
4. **First FVG** - 70% transparency + solid border
5. **Other FVGs** - 85% transparency + dashed border
6. **BSL/SSL** - Dotted lines with text labels (0.15 ATR offset)
7. **Order Blocks** - Yellow → Olive → Gray progression
8. **Session Lines** - Color-coded by session

## Best Practices

### ✅ DO
- Wait for ALL setup conditions
- Trade during SB windows only
- Watch Yesterday's Daily H/L for targets/stops
- Use 4H levels for secondary confirmation
- Monitor FVG 50% midline for precision entries
- Trust First FVG (most significant)
- Let dynamic settings adapt automatically

### ❌ DON'T
- Trade outside SB windows
- Force trades when HTF bias mixed
- Ignore liquidity sweeps
- Enter without FVG retracement
- Overtrade (expect 1-3 trades/week max)

## ICT Concepts Implemented
1. Kill Zones (London/NY AM/NY PM)
2. Silver Bullet (1-hour precision window)
3. Liquidity Sweeps (inter + intra session)
4. Fair Value Gaps (imbalance zones)
5. Market Structure Shift (trend confirmation)
6. Premium/Discount (value areas)
7. Order Blocks (last opposing candle)
8. HTF Macro Liquidity (Daily/4H reference)

## Technical Details
- **Pine Script v6** - Indicator with overlay
- **500 boxes, 500 lines** - Extensive history support
- **7 TF-adaptive settings** - Auto-scale across all timeframes
- **HTF data sources** - Daily, 4H, Weekly, Monthly
- **CPU optimized** - Lifecycle management + skip logic

## Performance Expectations
- **Setups**: 15-30 quality trades/year (highly selective)
- **Win Rate**: 60-75% (ICT methodology average)
- **Risk:Reward**: 2:1 to 3:1
- **Profit Factor**: 2.0+ with disciplined execution

## Credits
Based on ICT (Inner Circle Trader) mentorship concepts:
- Silver Bullet methodology
- Session-based liquidity sweeps
- Fair Value Gap entry models
- Market Structure principles

---

**⚠️ Disclaimer**: Educational tool only. All trading decisions are user's responsibility. Past performance doesn't guarantee future results. Use proper risk management.

**📜 Copyright**: All rights reserved. Unauthorized distribution prohibited.
