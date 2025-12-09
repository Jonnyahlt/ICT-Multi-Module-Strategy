# ICT Session Engine [Silver Bullet] - Professional Trading Strategy

## Overview
A complete ICT (Inner Circle Trader) Silver Bullet strategy implementation for TradingView, designed for institutional-style trading on NQ, ES, and other major indices. This script combines multiple ICT concepts into a systematic, rule-based approach with professional risk management.

## Core Methodology: The Silver Bullet Setup

The Silver Bullet is ICT's precision entry model that targets institutional order flow during specific time windows. The complete setup requires:

1. **Higher Timeframe Bias** - Direction confirmation from Daily/Weekly/Monthly EMAs
2. **Liquidity Sweep** - Session high/low violation that traps retail traders
3. **Market Structure Shift (MSS)** - Break of structure confirming reversal
4. **Fair Value Gap (FVG)** - Imbalance zone for precise entry
5. **Premium/Discount Zone** - Entry only in favorable price areas
6. **Silver Bullet Window** - 1-hour institutional killzone entry period

## Key Features

### 📊 Session-Based Structure
- **Asia Session** (20:00-00:00 ET): Range building phase
- **London Session** (02:00-05:00 ET): Setup phase, sweeps Asia range
- **NY AM Session** (09:30-11:00 ET): Primary killzone (highest probability)
- **NY PM Session** (13:30-16:00 ET): Secondary killzone (optional)

### 🎯 Silver Bullet Windows (Entry Times)
- **London SB**: 03:00-04:00 ET
- **NY AM SB**: 10:00-11:00 ET (most reliable)
- **NY PM SB**: 14:00-15:00 ET

### 💧 Dual Liquidity Sweep Detection
- **Inter-Session Sweeps**: London sweeps Asia, NY AM sweeps London (classic ICT)
- **Intra-Session Sweeps**: Session sweeps its own established high/low
- Dashboard shows sweep type: "(Prev)" for inter-session, "(Intra)" for intra-session

### 🎯 HTF Macro Liquidity Overlay
- **Yesterday's Daily High/Low**: Visual reference for major liquidity pools (thick solid lines)
- **4H Swing High/Low**: Secondary macro liquidity levels (dashed lines)
- **Label Placement**: Right-side, center-aligned for easy tracking throughout the day
- **Visual Hierarchy**: Daily (most important) → 4H (secondary) → Current TF liquidity
- **Zero Algorithm Impact**: Purely visual overlay - does not affect entry signals

### ⚙️ TF-Adaptive Dynamic Settings
- **FVG Max Age**: Auto-scales from Base×10 (1m) to Base×0.5 (Daily) - more bars on lower timeframes
- **OB Max Age**: Same scaling as FVG - keeps relevant blocks visible per timeframe
- **Premium/Discount Swing Strength**: Base×0.5 (1m fast swings) to Base×2.5 (Daily major swings)
- **Equal H/L Lookback**: Confirmation bars scale from 2 bars (1m) to 6 bars (Daily)
- **Liquidity Macro Threshold**: 1.0% (1m volatile) to 0.25% (Daily major swings)
- **MSS Lookback**: 50% reduction on 1H+ timeframes for faster structure detection
- **Concrete Examples in Tooltips**: Every dynamic setting shows exact values for each timeframe

### 📦 Advanced FVG Management
- ATR-adaptive sizing with 4 sensitivity levels (Extreme/High/Normal/Low)
- Manual minimum size override for precise control
- Bar type filtering (same direction candles = higher quality)
- Retracement requirement (wait for price to retrace into FVG)
- **First FVG of session**: 70% transparency, solid border, "#1" label (most significant)
- **Other FVGs**: 85% transparency, dashed border for visual hierarchy
- **50% Midline**: Dashed reference line at FVG midpoint for precision entries
- Age-based invalidation with dynamic TF scaling (200 bars on 1m, 10 bars on Daily)
- Performance optimized with managed lifecycle (no infinite lines)

### 📦 Order Block Detection
- **ICT-Compliant Logic**: Last opposing candle before strong engulfing move
- **Relaxed Criteria**: Detects either 2-bar momentum OR high/low break for balance
- **Quality Validation**: Wick ratio and body size checked after detection (inside processing)
- **Visual Hierarchy**: 
  - Fresh OB: Bright yellow candle (#FFEB3B, 0% transparency)
  - Breaker Block: Muted olive (#9E9D24, dashed border) - failed OB that flipped
  - Mitigated Block: Gray label when filled
- **Dynamic Age**: Base×10 on 1m (500 bars) to Base×0.5 on Daily (25 bars)
- **Optional Boxes**: Toggle OB box display (OFF = cleaner chart with candle color only)

### 🔄 Market Structure Detection
- Break of Structure (BOS) identification
- MSS visualization with horizontal lines
- Swing high/low tracking for liquidity pools

### 📈 Higher Timeframe Bias Alignment
- **Daily 50 EMA**: Primary institutional bias
- **Weekly 20 EMA**: Intermediate trend confirmation
- **Monthly 12 EMA**: Long-term directional bias
- **HTF Aligned**: All timeframes in sync = highest probability setups
- Dashboard shows alignment status with ⭐ indicator

### 💰 Professional Risk Management
- Fixed dollar risk per trade (default $400 for prop firms)
- ATR-based stop placement (adapts to volatility)
- Configurable Risk:Reward ratio (default 2:1)
- Trailing stop activation after 1:1 reward hit
- Position sizing calculated automatically

### 🎨 Visual Elements
- **Session Lines**: Color-coded (Purple=Asia, Red=London, Green=NY AM, Blue=NY PM)
- **Lines Start at Exact Bars**: High/low placement at actual bar (not session start)
- **HTF Macro Liquidity**: 
  - Yesterday's Daily H/L: Thick solid red/green lines (width 3) with "MACRO BSL/SSL (Yesterday)" labels
  - 4H Swing H/L: Medium dashed lines (width 2, 30% transparency) with "MACRO BSL/SSL (4H)" labels
  - Labels: Right-side, center-aligned, follow price throughout day
- **FVG Visual Hierarchy**: 
  - First FVG: 70% transparency, solid border, thicker, "#1" label
  - Other FVGs: 85% transparency, dashed border
  - 50% Midline: Dashed line at midpoint for precision
- **Order Block Colors**: Yellow (fresh) → Olive (breaker) → Gray (mitigated)
- **Mitigation Behavior**: Control line continuation after violation
- **Daily Reset**: Time picker for automatic visual cleanup (default 18:00 ET)
- **MSS Markers**: Orange lines with arrows
- **Liquidity Levels**: BSL/SSL dotted lines with macro hierarchy

### 🔔 Alert System
- "Long SB Setup" - All long conditions met
- "Short SB Setup" - All short conditions met
- "HTF Bias Aligned" - Daily/Weekly/Monthly all in sync during SB window

### 📱 Real-Time Dashboard
Displays current status:
- Active session and SB window
- Daily/Weekly/Monthly bias
- HTF alignment status (⭐ when all aligned)
- Premium/Discount zone
- Session ranges
- Liquidity sweep status (with type: Prev/Intra)
- Active FVGs with quality indicator
- Risk per trade
- Setup checklist (HTF Bias → Liq Sweep → MSS → FVG)

## Entry Rules

### Long Setup
```
✓ HTF Bias Bullish (Daily/Weekly/Monthly above EMAs)
✓ SSL Swept (session low violated)
✓ MSS Bullish (break above recent high)
✓ Price in Discount Zone (below 50% of daily range)
✓ FVG Retraced (price returned into bullish FVG)
✓ Inside Silver Bullet Window (SB hour active)
```

### Short Setup
```
✓ HTF Bias Bearish (Daily/Weekly/Monthly below EMAs)
✓ BSL Swept (session high violated)
✓ MSS Bearish (break below recent low)
✓ Price in Premium Zone (above 50% of daily range)
✓ FVG Retraced (price returned into bearish FVG)
✓ Inside Silver Bullet Window (SB hour active)
```

## Configuration

### Recommended Settings
- **Symbol**: NQ1!, ES1!, or other major indices
- **Timeframe**: 1-minute to Daily (all TF-adaptive)
- **Primary Timeframes**: 5-minute (scalping) or 15-minute (swing)
- **Sessions**: Trade London SB + NY AM SB (highest probability)
- **Risk**: $400 per trade (adjust for account size)
- **Risk:Reward**: 2:1 minimum
- **FVG Sensitivity**: Normal (1.5x ATR)
- **FVG Retracement**: Required (ON)
- **HTF Macro Liquidity**: ON (visual context for major pools)
- **Dynamic Settings**: Use Base values (20/50/3/0.5) - auto-scales per timeframe

### Performance Optimization
- `max_boxes_count=500` - Handles extensive FVG history
- `max_lines_count=500` - Supports multiple session lines
- FVG loop skips box updates for expired FVGs (CPU optimization)

### Visual Controls
- **Show Session Boxes**: Display session high/low lines
- **Show FVG Zones**: Display Fair Value Gap boxes with midlines
- **Show Liquidity Levels**: Display BSL/SSL levels
- **Show Macro HTF Liquidity**: Display Yesterday's Daily + 4H swing levels
- **Show Order Blocks**: Display OB candle coloring and labels
- **Show OB Boxes**: Toggle box display around OBs (OFF = cleaner)
- **Show Entry Labels**: Display LONG/SHORT markers on entries
- **Extend Mitigated Lines**: Continue or stop lines after violation
- **Daily Reset**: Clear all visuals at specified time (default 18:00 ET)

## Backtest Results (Expected)
- **Trading Days**: ~250/year
- **Setups**: 15-30 quality trades/year (highly selective)
- **Win Rate**: 60-75% (ICT methodology average)
- **Risk:Reward**: 2:1 to 3:1
- **Profit Factor**: 2.0+ (with disciplined execution)

## Best Practices

### ✅ DO
- Wait for ALL setup conditions before entry
- Trade during Silver Bullet windows only
- Focus on NY AM SB (highest probability)
- Require HTF bias alignment for strongest setups
- **Watch Yesterday's Daily H/L**: Major liquidity magnets for targets/stops
- **Use 4H Swing Levels**: Secondary confirmation for entries/exits
- **Monitor FVG 50% Midline**: Precision entry zone within larger FVG
- **Trust First FVG**: Most significant imbalance after structure shift
- Use Daily Reset to maintain clean charts
- Trust inter-session sweeps (Prev) over intra-session
- Let dynamic settings adapt - no manual TF adjustments needed

### ❌ DON'T
- Trade outside SB windows (lower probability)
- Force trades when HTF bias is mixed
- Ignore liquidity sweeps (critical component)
- Enter without FVG retracement
- Overtrade (expect 1-3 trades per week max)

## ICT Concepts Implemented

1. **Kill Zones** - Institutional trading windows (London/NY AM/NY PM)
2. **Silver Bullet** - Precision 1-hour entry window
3. **Liquidity Sweeps** - Stop hunts that reverse (inter + intra session)
4. **Fair Value Gaps** - Imbalance zones with retracement logic
5. **Market Structure Shift** - Trend change confirmation
6. **Premium/Discount** - Value area pricing (50% of daily range)
7. **Session Highs/Lows** - Liquidity reference points
8. **Power of Three** - Accumulation → Manipulation → Distribution

## Technical Specifications
- **Pine Script Version**: v6
- **Indicator Type**: Overlay with multi-timeframe data
- **Max Objects**: 500 boxes, 500 lines (optimized for extensive history)
- **TF-Adaptive Engine**: 7 dynamic settings auto-scale across all timeframes
- **HTF Data Sources**: Daily, 4H, Weekly, Monthly security calls
- **Performance**: CPU optimized with lifecycle management and skip logic
- **Visual Layers**: Session boxes, FVG zones, OB coloring, HTF macro lines, liquidity levels
- **Label Management**: Persistent labels with position updates (right-side tracking)

## Use Cases
- **Prop Firm Challenges**: Conservative, rule-based approach for passing evaluations
- **Live Trading**: Systematic entries during institutional hours
- **Backtesting**: Historical performance validation on 2+ years of data
- **Education**: Learn ICT concepts with visual confirmation

## Credits
Based on ICT (Inner Circle Trader) mentorship concepts, specifically:
- Silver Bullet methodology
- Session-based liquidity sweeps
- Fair Value Gap entry models
- Market Structure principles

## Support
For questions about ICT concepts, refer to ICT's 2022 Mentorship series on YouTube.

---

**Disclaimer**: This strategy is for educational purposes. Past performance does not guarantee future results. Always practice proper risk management and use appropriate position sizing for your account.
**⚠️ Disclaimer**: Detta är ett tekniskt analysverktyg. Alla tradingbeslut är användarens eget ansvar. Historisk performance är ingen garanti för framtida resultat. Använd alltid proper risk management.

**📜 Copyright**: All rights reserved. Unauthorized distribution prohibited.
