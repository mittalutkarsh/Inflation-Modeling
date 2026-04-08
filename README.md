# Bond Market Stagflation Scenario Model

> A live Excel workbook for monitoring, decomposing, and simulating the inflation-vs-recession tug of war in global bond markets during the 2026 Iran war / Strait of Hormuz crisis.

[![Excel](#)](#)
[![Data Sources](#data-sources)](#data-sources)
[![License](#license)](#license)

---

## Overview

The closure of the Strait of Hormuz in March 2026 triggered the largest oil supply disruption in history, sending Brent crude from **$61 to $126 per barrel** and whipsawing government bond yields globally.

Bond markets are being pulled by two opposing forces:

- **Inflation** → pushes yields higher through purchasing power compensation and rate hike expectations
- **Recession** → pushes yields lower through flight-to-safety demand and rate cut expectations

This model helps you:

- track which force is currently dominating
- decompose yield movements into their underlying drivers
- simulate scenarios based on oil prices, disruption severity, and conflict duration

**Companion article:** *Bonds Are Screaming Two Things at Once — And Both Are Terrifying*  
*(Insert Medium link here)*

---

## Workbook Structure

The workbook contains **5 sheets**, each designed for a specific analytical purpose.

### 1. Data Pull

**Purpose:**  
Reference sheet containing FRED series codes, direct CSV download URLs, and setup instructions for auto-refreshing data.

**Includes 15 time series, such as:**

| Series | FRED Code | Frequency |
|---|---|---|
| US 10Y Treasury Yield | DGS10 | Daily |
| US 2Y Treasury Yield | DGS2 | Daily |
| 10Y–2Y Yield Spread | T10Y2Y | Daily |
| 10Y Breakeven Inflation | T10YIE | Daily |
| Brent Crude Oil | DCOILBRENTEU | Daily |
| Fed Funds Rate | DFF | Daily |
| US CPI | CPIAUCSL | Monthly |
| UK Gilt Yield | IRLTLT01GBM156N | Monthly |
| Germany Bund Yield | IRLTLT01DEM156N | Monthly |

**Refresh options:**

- **FRED Excel Add-In** *(recommended)*: Download the add-in → open the **FRED** tab → **Build Dataset** → **Refresh**
- **Power Query**: `Data` → `Get Data` → `From Web` → paste the CSV URL from the sheet
- **Direct CSV import**: each URL returns a `.csv` file that can be imported manually

---

### 2. Dashboard

**Purpose:**  
A high-level snapshot comparing current market levels against pre-war baselines from **February 27**.

**Tracks:**

- US, UK, German, and Japanese 10Y yields
- Brent crude oil price
- 10Y–2Y yield spread
- 10Y breakeven inflation
- Fed Funds Rate

**Auto-calculated fields:**

- **Change** = `Current − Pre-War`
- **Signal** = `↑ RISING` / `↓ FALLING` / `— FLAT`

**Interpretation rules included**, for example:

> If Brent > $120 and breakeven inflation > 3.0%, inflation expectations may be unanchoring.

**Manual action required:**  
Update the **yellow cells** with the latest values after refreshing data.

---

### 3. Yield Decomposition

**Purpose:**  
Breaks the 10Y nominal Treasury yield into its three core components:

```text
10Y Nominal Yield = Real Yield (TIPS) + Breakeven Inflation + Term Premium



**Why it matters:**
This sheet identifies what is actually driving the move in nominal yields.

If breakeven inflation rises faster than the real yield, inflation fears are dominating
If the real yield rises while breakeven inflation is stable, the move is more likely a growth or term-premium story

Danger threshold:

Breakeven inflation > 3.0% → inflation expectations may be unanchoring
4. Scenario Simulator

Purpose:
Lets you input assumptions and estimate the resulting effects on inflation, bond yields, and growth.

User-editable inputs (11 parameters):
