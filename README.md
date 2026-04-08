Bond Market Stagflation Scenario Model
> A live Excel workbook for monitoring, decomposing, and simulating the inflation-vs-recession tug of war in global bond markets during the 2026 Iran war / Strait of Hormuz crisis.
[!Excel](#)
[!Data](#data-sources)
[!License](#license)
***Context
The closure of the Strait of Hormuz in March 2026 triggered the largest oil supply disruption in history, sending Brent crude from $61 to $126/bbl and whipsawing government bond yields globally. Bond markets are caught between two opposing forces:
Inflation → pushes yields up (compensation for purchasing power erosion + rate hike expectations)
Recession → pushes yields down (flight to safety + rate cut expectations)
This model helps you track which force is winning, decompose yield movements into their components, and simulate scenarios based on oil prices and conflict duration.
Companion article: Bonds Are Screaming Two Things at Once — And Both Are Terrifying (link to your Medium post)
***Workbook Structure
The model has 5 sheets, each serving a distinct purpose:
📋 Sheet 1: Data Pull
What: Reference sheet with FRED series codes, direct CSV download URLs, and setup instructions for auto-refreshing data.
Covers 15 series including:
| Series | FRED Code | Frequency |
|--------|-----------|-----------|
| US 10Y Treasury Yield | DGS10 | Daily |
| US 2Y Treasury Yield | DGS2 | Daily |
| 10Y–2Y Yield Spread | T10Y2Y | Daily |
| 10Y Breakeven Inflation | T10YIE | Daily |
| Brent Crude Oil | DCOILBRENTEU | Daily |
| Fed Funds Rate | DFF | Daily |
| US CPI | CPIAUCSL | Monthly |
| UK Gilt Yield | IRLTLT01GBM156N | Monthly |
| Germany Bund Yield | IRLTLT01DEM156N | Monthly |
How to refresh:
FRED Excel Add-In (recommended): Download here → FRED tab → Build Dataset → Refresh
Power Query: Data → Get Data → From Web → paste the CSV URL from the sheet
Direct CSV: each URL returns a .csv file you can import manually
📊 Sheet 2: Dashboard
What: At-a-glance snapshot comparing current market levels to pre-war (Feb 27) baselines.
Key metrics tracked:
US, UK, German, Japanese 10Y yields
Brent crude oil price
10Y–2Y yield spread (auto-calculated)
Breakeven inflation rate
Fed Funds Rate
Auto-calculated columns:
Change = Current − Pre-War
Signal = ↑ RISING / ↓ FALLING / — FLAT
Includes interpretation rules (e.g., "If Brent > $120 AND breakeven > 3% → DANGER ZONE: inflation expectations unanchoring")
Action required: Update the yellow cells with current values when you refresh data.
🔬 Sheet 3: Yield Decomposition
What: Breaks the 10Y nominal yield into its three components:
10Y Nominal = Real Yield (TIPS) + Breakeven Inflation + Term Premium
Why it matters: Tells you what's driving yield moves. If breakeven inflation is rising faster than the real yield, inflation fears dominate. If the real yield is rising while breakeven is stable, it's a growth/term premium story.
Danger threshold: Breakeven > 3.0% = inflation expectations may be unanchoring.
🎮 Sheet 4: Scenario Simulator
What: Input your assumptions in yellow cells, and the model projects impacts on inflation, yields, and growth.
Inputs (11 adjustable parameters):
| Input | Default | Description |
|-------|---------|-------------|
| Brent Crude Price | $110/bbl | Current or projected oil price |
| Conflict Duration | 3 months | Remaining months of disruption |
| Hormuz Flow Restoration | 10% | 0% = fully closed, 100% = open |
| OPEC+ Spare Capacity | 0.5 mb/d | Additional OPEC+ output |
| SPR Release Rate | 0.3 mb/d | Strategic reserve drawdown |
| Baseline CPI YoY | 2.4% | Pre-war inflation rate |
| Baseline 10Y Yield | 3.98% | Pre-war Treasury yield |
| Baseline GDP Growth | 2.4% | Pre-war growth projection |
| Inflation-to-Yield Beta | 0.65 | Historical sensitivity |
| Oil-to-CPI Passthrough | 0.04 | Each $10/bbl ≈ 0.4pp CPI |
| Energy Share of CPI | 7.5% | BLS CPI weight |
Auto-calculated outputs:
Projected CPI, 10Y yield, GDP growth
Net supply disruption (mb/d) and cumulative barrels lost
Stagflation Score with plain-English verdict:
🔴 Severe Stagflation
🟡 Moderate Stagflation  
🟢 Balanced / Maximum Uncertainty
🔵 Recession Risk Dominates
5 pre-built scenarios included (Quick Resolution, Base Case, Prolonged Closure, Escalation, OECD Downside) — copy values into yellow cells to run.
🚦 Sheet 5: Signal Monitor
What: Scorecard that tallies inflation signals vs. recession signals to determine the current market regime.
6 Inflation Signals:
10Y breakeven > 2.5%
Brent crude > $100/bbl
CPI YoY > 2.0% (Fed target)
Import prices MoM > 0.5%
OECD inflation revision > +1pp
2Y yield rising faster than 10Y (bear flattening)
6 Recession Signals:
10Y–2Y spread < 0 (yield curve inversion)
OECD growth revision < −0.3pp
Consumer confidence below average
Initial jobless claims > 250k
ISM Manufacturing < 50
Visible oil demand destruction
Net Verdict: Inflation Score − Recession Score → regime classification + positioning recommendation.
***Data Sources
All data is sourced from free, publicly available feeds:
| Source | URL | What It Provides |
|--------|-----|------------------|
| FRED (St. Louis Fed) | fred.stlouisfed.org | Treasury yields, spreads, inflation, oil prices, GDP |
| FRED Excel Add-In | fred.stlouisfed.org/fred-addin | One-click data refresh inside Excel |
| US Treasury | treasury.gov/resource-center | Daily par yield curve rates |
| EIA | eia.gov | Petroleum market reports & crude prices |
| OECD | oecd.org/economic-outlook | Growth & inflation forecasts (updated semi-annually) |
| CME FedWatch | cmegroup.com/fedwatch | Fed rate probabilities (manual input) |
Combined FRED Download URL
Pull multiple series in one request:
https://fred.stlouisfed.org/graph/fredgraph.csv?id=DGS10,DGS2,T10Y2Y,T10YIE,DFII10,DFF,DCOILBRENTEU,DCOILWTICO
Add a date range:
https://fred.stlouisfed.org/graph/fredgraph.csv?id=DGS10,DGS2,T10Y2Y&cosd=2025-01-01&coed=2026-12-31
***Quick Start
1. Open bond_market_model.xlsx
2. Go to "Data Pull" sheet → follow instructions to set up auto-refresh
3. Update yellow cells in "Dashboard" with latest values
4. Check "Signal Monitor" for current regime verdict
5. Use "Scenario Simulator" to test what-if scenarios
Refresh Workflow (Weekly Recommended)
Refresh data via FRED Add-In or Power Query
Update Dashboard yellow cells with latest values
Update Yield Decomposition with latest TIPS/breakeven data
Update Signal Monitor current values
Check Scenario Simulator verdict — adjust oil price assumption if needed
***Color Coding Convention
| Color | Meaning |
|-------|---------|
| 🟦 Blue text | Input cells — hardcoded values you update |
| ⬛ Black text | Formulas — auto-calculated, don't edit |
| 🟨 Yellow background | Editable assumptions — change these for scenarios |
***Formula Reference
Key formulas used in the Scenario Simulator:
| Output | Formula Logic |
|--------|---------------|
| CPI Impact | Oil_Price_Change × Oil_to_CPI_Passthrough |
| Projected CPI | Baseline_CPI + CPI_Impact |
| Yield Change | CPI_Impact × Inflation_to_Yield_Beta |
| GDP Drag | MAX(0, (Oil_Price − 80) × 0.005) |
| Net Supply Disruption | 10 × (1 − Hormuz_Flow%) − OPEC_Response − SPR_Release |
| Stagflation Score | Inflation_Impact − GDP_Drag (positive = inflation wins) |
***Limitations
Not financial advice. This is an analytical framework, not a trading signal.
Betas are estimates. The inflation-to-yield and oil-to-CPI coefficients are based on historical averages and will vary by regime.
Manual refresh required for CME FedWatch probabilities and OECD forecasts (not available via FRED API).
UK and German yields are monthly frequency on FRED; for daily data, use Bloomberg or Investing.com.
No VBA or macros. All formulas are standard Excel — works on Mac, Windows, and Google Sheets (with minor formatting differences).
***Related
📝 Medium Article: Bonds Are Screaming Two Things at Once — And Both Are Terrifying
📊 Charts: 6 original figures (bond yields, oil prices, OECD revisions, tug-of-war diagram, Fed expectations, growth forecasts)
🌐 OECD Interim Outlook (Mar 2026): oecd.org
📈 FRED 10Y Yield: fred.stlouisfed.org/series/DGS10
***License
MIT — use freely, attribution appreciated.
