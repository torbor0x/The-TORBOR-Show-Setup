# The Torbor Show Setup

A cleaned, documented, and GitHub-ready multi-confirmation TradingView Pine Script strategy.

**Pine Script v6** | Overlay | Strategy  
Designed primarily for the **5-minute timeframe**.

## Features

- **Entry logic** combines:
  - Supertrend direction flips
  - WaveTrend green/red signals (crosses in oversold/overbought zones)
  - Price position relative to 200 MA (chart + 1-minute), 21 SMA, and a 20-period high/low channel  
    (blue upper / orange lower lines with cyan fill — see Chart Visuals below)
  - RSI < 50 filter (longs) and MACD confirmation
- **Risk management**: ATR-based stop-loss and take-profit (set on entry)
- **Counter-signal exits**
- Clean visual signals (no circle dots, no 1m cross markers)
- Anti-clutter controls (`show_last`, toggle switches)
- Works on free TradingView accounts

## Chart Visuals

All of the following are plotted on the price chart:

| Plot                  | Color          | Description                                      |
|-----------------------|----------------|--------------------------------------------------|
| 200 MA                | Yellow         | Main trend filter (SMA or EMA, user choice)      |
| 1m 200 MA             | Red            | Same length MA calculated on the 1-minute TF     |
| 800 MA                | Light gray     | Longer-term MA on the chart timeframe            |
| 15m 800 MA            | White          | Same long MA calculated on the 15-minute TF      |
| 50 SMA                | Cyan           | Medium-term moving average                       |
| 21 SMA                | Purple         | Short-term moving average                        |
| Upper 20 SMA (high)   | Blue           | Upper edge of the 20-period high/low channel     |
| Lower 20 SMA (low)    | Orange         | Lower edge of the 20-period high/low channel     |
| Channel fill          | Cyan (transparent) | Fill between the upper and lower 20 SMAs     |
| Supertrend            | Green / Red    | Green when bullish, red when bearish             |

### Signal markers (toggleable, limited by “Max Signals to Show”)

| Signal                 | Shape            | Color          | Location     |
|------------------------|------------------|----------------|--------------|
| Long Entry             | Triangle up      | Green          | Below bar    |
| Short Entry            | Triangle down    | Red            | Above bar    |
| Chart 200 MA Cross     | Small diamond    | Aqua (bull) / Pink (bear) | Below / Above |

All signal plots can be turned on/off individually in the **Display & Signals** input group.

## Installation

1. Open TradingView → Pine Editor
2. Create a new script
3. Copy the entire contents of `The_Torbor_Show_Setup.pine`
4. Paste and click **Add to chart**
5. Recommended chart: 5-minute timeframe

## Inputs Overview

- **Display & Signals**: Toggle entry triangles and chart 200 MA crosses, limit historical shapes
- **RSI / MACD / Moving Averages**: Standard parameters
- **WaveTrend**: Channel/average lengths and OB/OS levels
- **Supertrend**: Factor and ATR period
- **Risk Management**: ATR length + SL/TP multipliers

## Free TradingView Compatibility

- The script is fully functional on free accounts.
- All indicators, plots, and strategy logic work without restriction.

## Strategy Logic Summary

**Long** when all of the following are true:
- Supertrend flips bullish
- Close > 200 MA (chart), 1m 200 MA, 21 SMA, and lower channel (orange line)
- WaveTrend green signal (cross in oversold)
- RSI < 50
- MACD line > signal line

**Short** is the inverse (bearish Supertrend flip + red WaveTrend signal + price below key MAs, etc.).

On a valid opposite signal the current position is closed.

Stop-loss and take-profit are ATR-based and set once when the position is opened.

## Alerts

The script includes `alert()` calls for:
- Long / Short entry signals
- Chart timeframe 200 MA crosses

## Disclaimer

This script is provided for **educational and research purposes only**.  
It is **not** financial advice. Trading involves substantial risk of loss.  
Always backtest thoroughly, understand the logic, and use proper risk management.  
Past performance does not guarantee future results.

## Improvements in this version (v1.3)

- Renamed to **The Torbor Show Setup**
- Removed 1-minute MA cross markers (diamonds and background highlights) to reduce chart crowding
- Removed related inputs, alerts, and lower-timeframe request
- Upgraded to Pine Script v6
- Fixed syntax error in background color logic (line continuation)
- Restored visible upper (blue) and lower (orange) 20-period channel lines with cyan fill
- Removed all circle dots / labels
- Replaced with clean triangles (entries) and small diamonds (chart MA crosses only)
- Added anti-clutter controls (`show_last`, individual toggles)
- Grouped and documented inputs
- Added extensive code comments and header documentation
- Improved structure and readability for open-source sharing
- Explicit free-plan notes
- Minor cleanups (lookahead_off, pyramiding=0, explicit margins, better variable scoping, etc.)

## License

MIT License (or adapt as desired). Feel free to fork, modify, and improve.

---

**Ready for GitHub.**  
Recommended structure:
```
/
├── The_Torbor_Show_Setup.pine
├── README.md
└── LICENSE (optional)
```
