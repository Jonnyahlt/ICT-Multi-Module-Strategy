# ICT Strategy - Pine Script Trading System

## Project Overview
This is a modular TradingView Pine Script system implementing ICT (Inner Circle Trader), TTrades, and LumiTrades concepts. The architecture is designed for independent module development with integration through a confluence engine.

## Architecture

### Core Modules (8 Total)
1. **Order Block Detector** - Identifies bullish/bearish OBs with strength grading (weak/medium/strong)
2. **Fair Value Gap Finder** - ICT-compliant FVG detection with gap inclusion logic
3. **Break of Structure + MSS** - Trend identification with volume filtering
4. **Liquidity Pool Locator** - Stop-hunt area detection at swing highs/lows
5. **Po3 / Fractal Momentum** - Power of Three phases (Accumulation → Manipulation → Expansion)
6. **Multi-TF Confluence Engine** - Weighted signal aggregation (OB=30%, FVG=20%, BOS=20%, Liquidity=20%, Po3=10%)
7. **Composite Risk Manager** - ATR-based stops/targets with volatility-adjusted position sizing
8. **Visual & Alert Layer** - Color-coded zones with auto-invalidation and time-based zone extension

### Key Design Principles
- **Modularitet**: Each module can be tested independently before integration
- **Multi-Timeframe Support**: All modules support M15, H1, H4, D1 aggregation
- **Confidence Scoring**: Confluence engine returns 0-100 score for trade suggestions
- **Zone Invalidation**: FVG/OB zones auto-remove when broken or filled
- **Full Configurability**: All parameters exposed via `input()` settings

## Pine Script Conventions

### Module Structure Pattern
```pine
// ============================================================================
// MODULE X: [Module Name]
// ============================================================================

// --- Input Parameters ---
i_moduleX_enabled = input.bool(true, "Enable Module X", group="Module X")
i_moduleX_param1 = input.int(14, "Parameter 1", minval=1, group="Module X")

// --- Detection Logic ---
[function definitions with clear comments]

// --- Zone Drawing ---
[box/line drawing with color coding and invalidation]
```

### Naming Conventions
- **Inputs**: Prefix with `i_` (e.g., `i_ob_lookback`)
- **Functions**: Descriptive names (e.g., `detectOrderBlock()`, `calculateFVG()`)
- **Colors**: Use `color.new()` with transparency for zones (e.g., `color.new(color.green, 85)`)
- **Strength Levels**: Enum-like approach with constants (WEAK=1, MEDIUM=2, STRONG=3)

### Critical Definitions

**Order Block (OB)**:
- Last down-candle before bullish engulfing (bullish OB)
- Last up-candle before bearish engulfing (bearish OB)
- Must have wick threshold validation

**Fair Value Gap (FVG)**:
- 3-candle pattern where candle[1] leaves gap between candle[0] and candle[2]
- Gap measured between wicks AND bodies
- If price gaps, include full gap in FVG zone

**Break of Structure (BOS)**:
- Price breaks most recent swing high (bullish) or low (bearish)
- Must meet minimum movement % threshold
- Volume confirmation required

## Development Workflow

### Testing Individual Modules
1. Copy module code into separate Pine Script file
2. Add minimal chart plotting for validation
3. Test on M15/H1/H4/D1 timeframes
4. Verify parameter adjustments via settings

### Integration Steps
1. All modules must use consistent data structures for signals
2. Confluence engine expects: `{type: string, strength: float, price: float, timeframe: string}`
3. Visual layer subscribes to confluence engine output (score >70 triggers alerts)
4. Risk manager calculates position size based on confluence score and ATR

### Build & Deploy
- Edit `ICT_Strategy.pine` - main file contains all integrated modules
- Copy/paste into TradingView Pine Editor (no compilation step needed)
- Apply to chart and configure via Settings → Inputs

## Key Files
- `ICT_Strategy.pine` - Main integrated script with all 8 modules
- `.github/copilot-instructions.md` - This file (agent guidance)

## Common Patterns

### Multi-Timeframe Data Fetching
```pine
htf_high = request.security(syminfo.tickerid, "60", high[1], lookahead=barmerge.lookahead_on)
```

### Zone Drawing with Invalidation
```pine
if zone_is_broken
    box.delete(zone_box_id)
    array.remove(active_zones, zone_index)
```

### Time-Based Zone Extension
```pine
box.set_right(zone_box_id, bar_index + i_zone_extension_candles)
```

## AI Agent Guidelines
- **Always comment Swedish requirements in English** within code
- When adding features, maintain the 8-module structure
- Test FVG/OB detection logic against ICT video examples
- Confluence weights must total 100%
- Default risk per trade: 1% of account
- Zone colors: Green (long), Red (short), Blue (neutral), Yellow (confluence)

## Resources
- ICT Concepts: Focus on 2022 mentorship series for OB/FVG definitions
- Pine Script v5 Reference: https://www.tradingview.com/pine-script-reference/v5/
