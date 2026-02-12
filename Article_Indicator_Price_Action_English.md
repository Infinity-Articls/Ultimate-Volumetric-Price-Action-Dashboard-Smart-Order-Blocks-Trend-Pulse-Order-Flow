# Comprehensive Guide to Price Action Volumetric OB & Trend Strength Indicator: A Revolution in Price Action and Liquidity Analysis

This indicator stands as one of the most powerful tools programmed in **Pine Script v5** on the **TradingView** platform. It seamlessly integrates three core concepts of professional trading: **Order Blocks (OB)**, **Price Action analysis**, and **Trend Strength**.

In this educational article, we will dive deep into the details of this indicator and provide a line-by-line analysis of its source code to empower developers and traders to understand the mathematical and logical foundation behind it.

---

## Part 1: Key Components of the Indicator

1.  **Volumetric Order Blocks:** The indicator identifies supply and demand zones with high precision, displaying the buy and sell activity percentages within each zone.
2.  **Trend Strength Gauge:** A visual tool at the bottom of the screen that illustrates the current momentum using advanced mathematical equations based on Weighted Moving Averages (WMA).
3.  **Volume Orderbook:** A visual representation of volume distribution at various price levels around the current price, helping identify hidden support and resistance levels.

---

## Part 2: Line-by-Line Code Analysis

### 1. Indicator Setup and Inputs (Lines 1 - 42)
The code begins by defining the version, naming the indicator, and setting limits for drawing elements (Lines, Boxes, Labels).

```pinescript
4: //@version=5
5: indicator("Price Action Volumetric OB & Trend Strength", overlay = true, ...)
```
*   **Line 5:** Defines the indicator with `overlay = true` to appear directly on the price chart.

```pinescript
21: obshow = input.bool(true, "Show Last", ...)
29: obmode = input.string("Length", "Construction", ["Length", "Full"], ...)
```
*   These lines define user inputs to control how Order Blocks are displayed and the method for calculating their precision (either by "Length" or the "Full" candle body).

### 2. Custom Data Structures (Types) (Lines 44 - 74)
Using the `type` feature in Pine Script v5 keeps the code organized and professional.

```pinescript
44: type bar
45:     float o = open
...
53: type ob
54:     float top
55:     float btm
56:     float avg
...
```
*   **`bar` type:** Stores current candle data (open, high, low, close, volume).
*   **`ob` type:** Stores properties of an Order Block zone (top, bottom, average price, color, and internal volume).

### 3. Display and Analysis Methods (Lines 82 - 166)
Here we see the true power of organization using the `method` keyword.

*   **`display` method:** Responsible for drawing the boxes and lines representing liquidity zones.
*   **`overlap` method:** Intelligently prevents zones from overlapping. It removes older zones if a new one covers their range, keeping the "Price Waterfall" clean.
*   **`umt` method:** Updates the coordinates of buy/sell activity (Price Action metrics) to ensure accurate drawing during time expansions.

### 4. Order Block Detection Logic (Lines 167 - 283)
This is the "brain" of the indicator.

```pinescript
172: up = ta.highest(len)
173: dn = ta.lowest(len)
174: pv = ta.pivothigh(b.v, len, len)
```
*   The indicator uses Pivots based on volume `b.v` and `highest`/`lowest` levels to identify potential reversals.

```pinescript
183: if pv and dir == 1 and blob.size() < obmaxsz
184:     new_ob = ob.new(topP, b.l[len], ...)
```
*   Upon detecting a pivot and meeting trend conditions, a new `ob` object is created and added to the active zones array.

### 5. Trend Strength Gauge (Lines 284 - 338)
This part works in a separate calculation (often displayed at the bottom) to measure momentum.

```pinescript
289: wma = ta.wma(close, length)
291: a = 3 * wma - 2 * wma1
293: diff = a - a1
```
*   Calculations are based on the difference between Wrapped Moving Averages (WMA) and Simple Moving Averages (SMA) to create a momentum equation similar to the Hull Moving Average for zero-lag responsiveness.

### 6. Volume Orderbook (Lines 340 - 520)
This section is highly advanced, sorting and distributing trading volumes across price levels.

```pinescript
405: for i = 0 to levels.size() - 2
408:     if src < lvl1 and src > lvl2
411:         volumes.set(v_idx, volumes.get(v_idx) + volume)
```
*   The code calculates price "steps," builds a grid of levels, and distributes each candle's volume across these levels.
*   Finally (Line 446), it renders these results as a histogram showing where liquidity is concentrated (POC - Point of Control).

---

## Part 3: How to Trade with This Indicator?

1.  **OB Zones:** Wait for the price to reach the drawn zone. If the zone is green and accompanied by an increase in internal buying activity, it’s a strong entry opportunity.
2.  **Strength Gauge:** Avoid entering trades against the trend if the gauge shows a strong color (Deep Teal for Bullish, White/Red for Bearish).
3.  **Liquidity Confirmation:** Use the Orderbook to set targets. High-volume areas (longer boxes) act as price magnets or solid support/resistance.

---

## Conclusion
The **Price Action Volumetric OB & Trend Strength** indicator is not just a simple drawing tool; it is a comprehensive market analysis system. The code reflects high professionalism in using data arrays and custom types, making it an excellent example of advanced programming in TradingView.

---
**Prepared by:** [Infinity Algo Academy]
**Official Product Link:** [Ultimate Volumetric Price Action Dashboard](https://infinityalgoacademy.net/item/ultimate-volumetric-price-action-dashboard-smart-order-blocks-trend-pulse-order-flow/)
**Join us for more tools:** [https://t.me/simpleforextools]
