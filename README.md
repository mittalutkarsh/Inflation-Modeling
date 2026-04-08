Bond Market Stagflation Scenario Model
A live Excel workbook for monitoring, decomposing, and simulating the inflation-vs-recession tug of war in global bond markets during the 2026 Iran war / Strait of Hormuz crisis.

📊 .xlsx
📡 FRED Data
📄 MIT
Context
The closure of the Strait of Hormuz in March 2026 triggered the largest oil supply disruption in history, sending Brent crude from $61 to $126/bbl and whipsawing government bond yields globally. Bond markets are caught between two opposing forces:

• Inflation → pushes yields up (compensation for purchasing power erosion + rate hike expectations)
• Recession → pushes yields down (flight to safety + rate cut expectations)

This model helps you track which force is winning, decompose yield movements into their components, and simulate scenarios based on oil prices and conflict duration.

Companion article: Bonds Are Screaming Two Things at Once — And Both Are Terrifying

Workbook Structure
The model has 5 sheets, each serving a distinct purpose:

📋 Sheet 1: Data Pull
Reference sheet with FRED series codes, direct CSV download URLs, and setup instructions for auto-refreshing data.

Series	FRED Code	Frequency
US 10Y Treasury Yield	DGS10	Daily
US 2Y Treasury Yield	DGS2	Daily
10Y–2Y Yield Spread	T10Y2Y	Daily
10Y Breakeven Inflation	T10YIE	Daily
10Y TIPS Real Yield	DFII10	Daily
Fed Funds Rate	DFF	Daily
Brent Crude Oil	DCOILBRENTEU	Daily
WTI Crude Oil	DCOILWTICO	Daily
US CPI (All Urban)	CPIAUCSL	Monthly
US PCE Price Index	PCEPI	Monthly
US Real GDP Growth	A191RL1Q225SBEA	Quarterly
UK 10Y Gilt Yield	IRLTLT01GBM156N	Monthly
Germany 10Y Bund	IRLTLT01DEM156N	Monthly
US Import Price Index	IR	Monthly
How to refresh:

FRED Excel Add-In (recommended): Download here → FRED tab → Build Dataset → Refresh
Power Query: Data → Get Data → From Web → paste CSV URL
Direct CSV: Each URL returns a .csv you can import manually
📊 Sheet 2: Dashboard
At-a-glance snapshot comparing current market levels to pre-war (Feb 27) baselines. Tracks US/UK/German/Japan 10Y yields, Brent crude, yield spread, breakeven inflation, and Fed Funds Rate. Auto-calculates change and directional signal.

Includes interpretation rules (e.g., "If Brent > $120 AND breakeven > 3% → DANGER ZONE").

🔬 Sheet 3: Yield Decomposition
Breaks the 10Y nominal yield into components:

10Y Nominal = Real Yield (TIPS) + Breakeven Inflation + Term Premium
If breakeven inflation is rising faster than the real yield → inflation fears dominate.
Danger threshold: breakeven > 3.0%.

🎮 Sheet 4: Scenario Simulator
Input your assumptions in yellow cells, model projects impacts automatically.

Input	Default	Description
Brent Crude Price	$110/bbl	Current or projected oil price
Conflict Duration	3 months	Remaining months of disruption
Hormuz Flow Restoration	10%	0% = fully closed, 100% = open
OPEC+ Spare Capacity	0.5 mb/d	Additional OPEC+ output
SPR Release Rate	0.3 mb/d	Strategic reserve drawdown
Baseline CPI YoY	2.4%	Pre-war inflation rate
Baseline 10Y Yield	3.98%	Pre-war Treasury yield
Baseline GDP Growth	2.4%	Pre-war growth projection
Inflation-to-Yield Beta	0.65	Historical sensitivity
Oil-to-CPI Passthrough	0.04	Each $10/bbl ≈ 0.4pp CPI
Energy Share of CPI	7.5%	BLS CPI weight
Outputs: Projected CPI, 10Y yield, GDP growth, net supply disruption, cumulative barrels lost, and a Stagflation Score with verdict (🔴 Severe / 🟡 Moderate / 🟢 Balanced / 🔵 Recession Risk).

5 pre-built scenarios included: Quick Resolution, Base Case, Prolonged Closure, Escalation, OECD Downside.

🚦 Sheet 5: Signal Monitor
Scorecard of 6 inflation signals vs 6 recession signals → net regime verdict + positioning recommendation.

Inflation Signals: Breakeven > 2.5%, Brent > $100, CPI > 2%, Import prices MoM > 0.5%, OECD revision > +1pp, Bear flattening

Recession Signals: Yield curve inversion, OECD growth revision < −0.3pp, Consumer confidence below avg, Jobless claims > 250k, ISM < 50, Demand destruction visible

Data Sources
Source	URL	Provides
FRED	fred.stlouisfed.org	Treasury yields, spreads, inflation, oil, GDP
FRED Add-In	fred.stlouisfed.org/fred-addin	One-click Excel refresh
US Treasury	treasury.gov	Daily par yield curve
EIA	eia.gov	Petroleum market reports
OECD	oecd.org	Growth & inflation forecasts
CME FedWatch	cmegroup.com	Fed rate probabilities
Combined FRED Download URL
https://fred.stlouisfed.org/graph/fredgraph.csv?id=DGS10,DGS2,T10Y2Y,T10YIE,DFII10,DFF,DCOILBRENTEU,DCOILWTICO
With date range:

https://fred.stlouisfed.org/graph/fredgraph.csv?id=DGS10,DGS2,T10Y2Y&cosd=2025-01-01&coed=2026-12-31
Quick Start
Open bond_market_model.xlsx
Go to Data Pull sheet → follow instructions to set up auto-refresh
Update yellow cells in Dashboard with latest values
Check Signal Monitor for current regime verdict
Use Scenario Simulator to test what-if scenarios
Color Coding
Blue text
— Input cells: hardcoded values you update
Black text
— Formulas: auto-calculated, don't edit
Yellow background
— Editable assumptions: change for scenarios
Key Formulas
Output	Logic
CPI Impact	Oil_Price_Change × Oil_to_CPI_Passthrough
Projected CPI	Baseline_CPI + CPI_Impact
Yield Change	CPI_Impact × Inflation_to_Yield_Beta
GDP Drag	MAX(0, (Oil_Price − 80) × 0.005)
Net Supply Disruption	10 × (1 − Hormuz_Flow%) − OPEC − SPR
Stagflation Score	Inflation_Impact − GDP_Drag
Limitations
⚠️ Not financial advice. This is an analytical framework, not a trading signal. Betas are historical estimates and will vary by regime. CME FedWatch and OECD forecasts require manual refresh. UK/German yields are monthly on FRED; use Bloomberg for daily. No VBA/macros — standard Excel formulas, works everywhere.
Related
📝 Medium Article: Bonds Are Screaming Two Things at Once — And Both Are Terrifying
📊 Charts: 6 original figures (bond yields, oil prices, OECD revisions, tug-of-war diagram, Fed expectations, growth forecasts)
🌐 OECD Interim Outlook (Mar 2026): oecd.org
📈 FRED 10Y Yield: fred.stlouisfed.org/series/DGS10
