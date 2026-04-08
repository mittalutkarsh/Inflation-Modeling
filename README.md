
# Bond Market Stagflation Scenario Model

> A live Excel workbook for monitoring, decomposing, and simulating the inflation-vs-recession tug of war in global bond markets during the 2026 Iran war / Strait of Hormuz crisis.

![Excel](https://img.shields.io/badge/Format-.xlsx-217346?logo=microsoftexcel&logoColor=white) ![Data](https://img.shields.io/badge/Data_Source-FRED-003DA5) ![License](https://img.shields.io/badge/License-MIT-yellow)

---
## Article
https://medium.com/p/b4b3b9199202/edit

## Context

The closure of the Strait of Hormuz in March 2026 triggered the largest oil supply disruption in history, sending Brent crude from $61 to $126/bbl and whipsawing government bond yields globally. Bond markets are caught between two opposing forces:

- **Inflation** → pushes yields **up** (compensation for purchasing power erosion + rate hike expectations)
- **Recession** → pushes yields **down** (flight to safety + rate cut expectations)

This model helps you track which force is winning, decompose yield movements into their components, and simulate scenarios based on oil prices and conflict duration.

**Companion article:** [Bonds Are Screaming Two Things at Once — And Both Are Terrifying](#) *(link to your Medium post)*

---

## Workbook Structure

The model has **5 sheets**, each serving a distinct purpose:

### 📋 Sheet 1: `Data Pull`

Reference sheet with FRED series codes, direct CSV download URLs, and setup instructions for auto-refreshing data.

| Series | FRED Code | Frequency |
|--------|-----------|-----------|
| US 10Y Treasury Yield | `DGS10` | Daily |
| US 2Y Treasury Yield | `DGS2` | Daily |
| 10Y–2Y Yield Spread | `T10Y2Y` | Daily |
| 10Y Breakeven Inflation | `T10YIE` | Daily |
| 10Y TIPS Real Yield | `DFII10` | Daily |
| Fed Funds Rate | `DFF` | Daily |
| Brent Crude Oil | `DCOILBRENTEU` | Daily |
| WTI Crude Oil | `DCOILWTICO` | Daily |
| US CPI (All Urban) | `CPIAUCSL` | Monthly |
| US PCE Price Index | `PCEPI` | Monthly |
| US Real GDP Growth | `A191RL1Q225SBEA` | Quarterly |
| UK 10Y Gilt Yield | `IRLTLT01GBM156N` | Monthly |
| Germany 10Y Bund | `IRLTLT01DEM156N` | Monthly |
| US Import Price Index | `IR` | Monthly |

**How to refresh:**
1. **FRED Excel Add-In** (recommended): [Download here](https://fred.stlouisfed.org/fred-addin/) → FRED tab → Build Dataset → Refresh
2. **Power Query**: Data → Get Data → From Web → paste CSV URL
3. **Direct CSV**: Each URL returns a `.csv` you can import manually

### 📊 Sheet 2: `Dashboard`

At-a-glance snapshot comparing current market levels to pre-war (Feb 27) baselines. Tracks US/UK/German/Japan 10Y yields, Brent crude, yield spread, breakeven inflation, and Fed Funds Rate. Auto-calculates change and directional signal.

Includes interpretation rules (e.g., "If Brent > $120 AND breakeven > 3% → DANGER ZONE").

### 🔬 Sheet 3: `Yield Decomposition`

Breaks the 10Y nominal yield into components:

```
10Y Nominal = Real Yield (TIPS) + Breakeven Inflation + Term Premium
```

If breakeven inflation is rising faster than the real yield → inflation fears dominate. Danger threshold: breakeven > 3.0%.

### 🎮 Sheet 4: `Scenario Simulator`

Input your assumptions in yellow cells, model projects impacts automatically.

**Inputs (11 adjustable):**

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

**Outputs:** Projected CPI, 10Y yield, GDP growth, net supply disruption, cumulative barrels lost, and a **Stagflation Score** with verdict (🔴 Severe / 🟡 Moderate / 🟢 Balanced / 🔵 Recession Risk).

**5 pre-built scenarios** included: Quick Resolution, Base Case, Prolonged Closure, Escalation, OECD Downside.

### 🚦 Sheet 5: `Signal Monitor`

Scorecard of 6 inflation signals vs 6 recession signals → net regime verdict + positioning recommendation.

**Inflation Signals:** Breakeven > 2.5%, Brent > $100, CPI > 2%, Import prices MoM > 0.5%, OECD revision > +1pp, Bear flattening

**Recession Signals:** Yield curve inversion, OECD growth revision < −0.3pp, Consumer confidence below avg, Jobless claims > 250k, ISM < 50, Demand destruction visible

---

## Data Sources

| Source | URL | Provides |
|--------|-----|----------|
| **FRED** | [fred.stlouisfed.org](https://fred.stlouisfed.org) | Treasury yields, spreads, inflation, oil, GDP |
| **FRED Add-In** | [fred.stlouisfed.org/fred-addin](https://fred.stlouisfed.org/fred-addin/) | One-click Excel refresh |
| **US Treasury** | [treasury.gov](https://home.treasury.gov/resource-center/data-chart-center/interest-rates/TextView?type=daily_treasury_yield_curve) | Daily par yield curve |
| **EIA** | [eia.gov](https://www.eia.gov/todayinenergy/) | Petroleum market reports |
| **OECD** | [oecd.org](https://www.oecd.org/en/topics/sub-issues/economic-outlook.html) | Growth & inflation forecasts |
| **CME FedWatch** | [cmegroup.com](https://www.cmegroup.com/markets/interest-rates/cme-fedwatch-tool.html) | Fed rate probabilities |

### Combined FRED Download URL

```
https://fred.stlouisfed.org/graph/fredgraph.csv?id=DGS10,DGS2,T10Y2Y,T10YIE,DFII10,DFF,DCOILBRENTEU,DCOILWTICO
```

With date range:

```
https://fred.stlouisfed.org/graph/fredgraph.csv?id=DGS10,DGS2,T10Y2Y&cosd=2025-01-01&coed=2026-12-31
```

---

## Quick Start

1. Open `bond_market_model.xlsx`
2. Go to **Data Pull** sheet → follow instructions to set up auto-refresh
3. Update yellow cells in **Dashboard** with latest values
4. Check **Signal Monitor** for current regime verdict
5. Use **Scenario Simulator** to test what-if scenarios

### Refresh Workflow (Weekly Recommended)

1. Refresh data via FRED Add-In or Power Query
2. Update `Dashboard` yellow cells with latest values
3. Update `Yield Decomposition` with latest TIPS/breakeven data
4. Update `Signal Monitor` current values
5. Check `Scenario Simulator` verdict — adjust oil price assumption if needed

---

## Color Coding

| Color | Meaning |
|-------|---------|
| 🟦 Blue text | Input cells — hardcoded values you update |
| ⬛ Black text | Formulas — auto-calculated, don't edit |
| 🟨 Yellow background | Editable assumptions — change for scenarios |

---

## Key Formulas

| Output | Logic |
|--------|-------|
| CPI Impact | `Oil_Price_Change × Oil_to_CPI_Passthrough` |
| Projected CPI | `Baseline_CPI + CPI_Impact` |
| Yield Change | `CPI_Impact × Inflation_to_Yield_Beta` |
| GDP Drag | `MAX(0, (Oil_Price − 80) × 0.005)` |
| Net Supply Disruption | `10 × (1 − Hormuz_Flow%) − OPEC − SPR` |
| Stagflation Score | `Inflation_Impact − GDP_Drag` |

---

## Limitations

- **Not financial advice.** Analytical framework, not a trading signal.
- **Betas are estimates.** Historical averages; will vary by regime.
- **Manual refresh** required for CME FedWatch and OECD forecasts.
- **UK/German yields** are monthly on FRED; use Bloomberg for daily.
- **No VBA/macros.** Standard Excel formulas — works on Mac, Windows, Google Sheets.

---

## Related

- 📝 **Medium Article:** *Bonds Are Screaming Two Things at Once — And Both Are Terrifying*
- 📊 **Charts:** 6 original figures (bond yields, oil prices, OECD revisions, tug-of-war diagram, Fed expectations, growth forecasts)
- 🌐 **OECD Interim Outlook (Mar 2026):** [oecd.org](https://www.oecd.org/en/publications/oecd-economic-outlook-interim-report-march-2026_d4623013-en.html)
- 📈 **FRED 10Y Yield:** [fred.stlouisfed.org/series/DGS10](https://fred.stlouisfed.org/series/DGS10)

---

## License

MIT — use freely, attribution appreciated.
</textarea>

<div class="container">

  <div class="copy-wrap">
    <button class="copy-btn" onclick="copyMD()">📋 Copy README.md</button>
  </div>

  <h1>Bond Market Stagflation Scenario Model</h1>
  <p class="tagline">A live Excel workbook for monitoring, decomposing, and simulating the inflation-vs-recession tug of war in global bond markets during the 2026 Iran war / Strait of Hormuz crisis.</p>

  <div class="badges">
    <span class="badge excel">📊 .xlsx</span>
    <span class="badge data">📡 FRED Data</span>
    <span class="badge license">📄 MIT</span>
  </div>

  <hr>

  <h2>Context</h2>
  <p>The closure of the Strait of Hormuz in March 2026 triggered the largest oil supply disruption in history, sending Brent crude from $61 to $126/bbl and whipsawing government bond yields globally. Bond markets are caught between two opposing forces:</p>
  <p>• <strong>Inflation</strong> → pushes yields <strong>up</strong> (compensation for purchasing power erosion + rate hike expectations)<br>
     • <strong>Recession</strong> → pushes yields <strong>down</strong> (flight to safety + rate cut expectations)</p>
  <p>This model helps you track which force is winning, decompose yield movements into their components, and simulate scenarios based on oil prices and conflict duration.</p>
  <p><strong>Companion article:</strong> <a href="#">Bonds Are Screaming Two Things at Once — And Both Are Terrifying</a></p>

  <hr>

  <h2>Workbook Structure</h2>
  <p>The model has <strong>5 sheets</strong>, each serving a distinct purpose:</p>

  <div class="sheet-card green">
    <h3>📋 Sheet 1: <code>Data Pull</code></h3>
    <p>Reference sheet with FRED series codes, direct CSV download URLs, and setup instructions for auto-refreshing data.</p>
    <table>
      <tr><th>Series</th><th>FRED Code</th><th>Frequency</th></tr>
      <tr><td>US 10Y Treasury Yield</td><td><code>DGS10</code></td><td>Daily</td></tr>
      <tr><td>US 2Y Treasury Yield</td><td><code>DGS2</code></td><td>Daily</td></tr>
      <tr><td>10Y–2Y Yield Spread</td><td><code>T10Y2Y</code></td><td>Daily</td></tr>
      <tr><td>10Y Breakeven Inflation</td><td><code>T10YIE</code></td><td>Daily</td></tr>
      <tr><td>10Y TIPS Real Yield</td><td><code>DFII10</code></td><td>Daily</td></tr>
      <tr><td>Fed Funds Rate</td><td><code>DFF</code></td><td>Daily</td></tr>
      <tr><td>Brent Crude Oil</td><td><code>DCOILBRENTEU</code></td><td>Daily</td></tr>
      <tr><td>WTI Crude Oil</td><td><code>DCOILWTICO</code></td><td>Daily</td></tr>
      <tr><td>US CPI (All Urban)</td><td><code>CPIAUCSL</code></td><td>Monthly</td></tr>
      <tr><td>US PCE Price Index</td><td><code>PCEPI</code></td><td>Monthly</td></tr>
      <tr><td>US Real GDP Growth</td><td><code>A191RL1Q225SBEA</code></td><td>Quarterly</td></tr>
      <tr><td>UK 10Y Gilt Yield</td><td><code>IRLTLT01GBM156N</code></td><td>Monthly</td></tr>
      <tr><td>Germany 10Y Bund</td><td><code>IRLTLT01DEM156N</code></td><td>Monthly</td></tr>
      <tr><td>US Import Price Index</td><td><code>IR</code></td><td>Monthly</td></tr>
    </table>
    <p><strong>How to refresh:</strong></p>
    <ol class="steps">
      <li><strong>FRED Excel Add-In</strong> (recommended): <a href="https://fred.stlouisfed.org/fred-addin/">Download here</a> → FRED tab → Build Dataset → Refresh</li>
      <li><strong>Power Query:</strong> Data → Get Data → From Web → paste CSV URL</li>
      <li><strong>Direct CSV:</strong> Each URL returns a <code>.csv</code> you can import manually</li>
    </ol>
  </div>

  <div class="sheet-card blue">
    <h3>📊 Sheet 2: <code>Dashboard</code></h3>
    <p>At-a-glance snapshot comparing current market levels to pre-war (Feb 27) baselines. Tracks US/UK/German/Japan 10Y yields, Brent crude, yield spread, breakeven inflation, and Fed Funds Rate. Auto-calculates change and directional signal.</p>
    <p>Includes interpretation rules (e.g., <em>"If Brent > $120 AND breakeven > 3% → DANGER ZONE"</em>).</p>
  </div>

  <div class="sheet-card purple">
    <h3>🔬 Sheet 3: <code>Yield Decomposition</code></h3>
    <p>Breaks the 10Y nominal yield into components:</p>
    <pre>10Y Nominal = Real Yield (TIPS) + Breakeven Inflation + Term Premium</pre>
    <p>If breakeven inflation is rising faster than the real yield → inflation fears dominate.<br>
    <strong>Danger threshold:</strong> breakeven &gt; 3.0%.</p>
  </div>

  <div class="sheet-card red">
    <h3>🎮 Sheet 4: <code>Scenario Simulator</code></h3>
    <p>Input your assumptions in yellow cells, model projects impacts automatically.</p>
    <table>
      <tr><th>Input</th><th>Default</th><th>Description</th></tr>
      <tr><td>Brent Crude Price</td><td>$110/bbl</td><td>Current or projected oil price</td></tr>
      <tr><td>Conflict Duration</td><td>3 months</td><td>Remaining months of disruption</td></tr>
      <tr><td>Hormuz Flow Restoration</td><td>10%</td><td>0% = fully closed, 100% = open</td></tr>
      <tr><td>OPEC+ Spare Capacity</td><td>0.5 mb/d</td><td>Additional OPEC+ output</td></tr>
      <tr><td>SPR Release Rate</td><td>0.3 mb/d</td><td>Strategic reserve drawdown</td></tr>
      <tr><td>Baseline CPI YoY</td><td>2.4%</td><td>Pre-war inflation rate</td></tr>
      <tr><td>Baseline 10Y Yield</td><td>3.98%</td><td>Pre-war Treasury yield</td></tr>
      <tr><td>Baseline GDP Growth</td><td>2.4%</td><td>Pre-war growth projection</td></tr>
      <tr><td>Inflation-to-Yield Beta</td><td>0.65</td><td>Historical sensitivity</td></tr>
      <tr><td>Oil-to-CPI Passthrough</td><td>0.04</td><td>Each $10/bbl ≈ 0.4pp CPI</td></tr>
      <tr><td>Energy Share of CPI</td><td>7.5%</td><td>BLS CPI weight</td></tr>
    </table>
    <p><strong>Outputs:</strong> Projected CPI, 10Y yield, GDP growth, net supply disruption, cumulative barrels lost, and a <strong>Stagflation Score</strong> with verdict (🔴 Severe / 🟡 Moderate / 🟢 Balanced / 🔵 Recession Risk).</p>
    <p><strong>5 pre-built scenarios</strong> included: Quick Resolution, Base Case, Prolonged Closure, Escalation, OECD Downside.</p>
  </div>

  <div class="sheet-card orange">
    <h3>🚦 Sheet 5: <code>Signal Monitor</code></h3>
    <p>Scorecard of 6 inflation signals vs 6 recession signals → net regime verdict + positioning recommendation.</p>
    <p><strong>Inflation Signals:</strong> Breakeven &gt; 2.5%, Brent &gt; $100, CPI &gt; 2%, Import prices MoM &gt; 0.5%, OECD revision &gt; +1pp, Bear flattening</p>
    <p><strong>Recession Signals:</strong> Yield curve inversion, OECD growth revision &lt; −0.3pp, Consumer confidence below avg, Jobless claims &gt; 250k, ISM &lt; 50, Demand destruction visible</p>
  </div>

  <hr>

  <h2>Data Sources</h2>
  <table>
    <tr><th>Source</th><th>URL</th><th>Provides</th></tr>
    <tr><td><strong>FRED</strong></td><td><a href="https://fred.stlouisfed.org">fred.stlouisfed.org</a></td><td>Treasury yields, spreads, inflation, oil, GDP</td></tr>
    <tr><td><strong>FRED Add-In</strong></td><td><a href="https://fred.stlouisfed.org/fred-addin/">fred.stlouisfed.org/fred-addin</a></td><td>One-click Excel refresh</td></tr>
    <tr><td><strong>US Treasury</strong></td><td><a href="https://home.treasury.gov/resource-center/data-chart-center/interest-rates/TextView?type=daily_treasury_yield_curve">treasury.gov</a></td><td>Daily par yield curve</td></tr>
    <tr><td><strong>EIA</strong></td><td><a href="https://www.eia.gov/todayinenergy/">eia.gov</a></td><td>Petroleum market reports</td></tr>
    <tr><td><strong>OECD</strong></td><td><a href="https://www.oecd.org/en/topics/sub-issues/economic-outlook.html">oecd.org</a></td><td>Growth & inflation forecasts</td></tr>
    <tr><td><strong>CME FedWatch</strong></td><td><a href="https://www.cmegroup.com/markets/interest-rates/cme-fedwatch-tool.html">cmegroup.com</a></td><td>Fed rate probabilities</td></tr>
  </table>

  <h3>Combined FRED Download URL</h3>
  <pre>https://fred.stlouisfed.org/graph/fredgraph.csv?id=DGS10,DGS2,T10Y2Y,T10YIE,DFII10,DFF,DCOILBRENTEU,DCOILWTICO</pre>
  <p>With date range:</p>
  <pre>https://fred.stlouisfed.org/graph/fredgraph.csv?id=DGS10,DGS2,T10Y2Y&cosd=2025-01-01&coed=2026-12-31</pre>

  <hr>

  <h2>Quick Start</h2>
  <ol class="steps">
    <li>Open <code>bond_market_model.xlsx</code></li>
    <li>Go to <strong>Data Pull</strong> sheet → follow instructions to set up auto-refresh</li>
    <li>Update yellow cells in <strong>Dashboard</strong> with latest values</li>
    <li>Check <strong>Signal Monitor</strong> for current regime verdict</li>
    <li>Use <strong>Scenario Simulator</strong> to test what-if scenarios</li>
  </ol>

  <hr>

  <h2>Color Coding</h2>
  <div class="color-row"><div class="color-swatch" style="background:#0000FF;"></div><strong>Blue text</strong> — Input cells: hardcoded values you update</div>
  <div class="color-row"><div class="color-swatch" style="background:#000;"></div><strong>Black text</strong> — Formulas: auto-calculated, don't edit</div>
  <div class="color-row"><div class="color-swatch" style="background:#FFF2CC; border-color:#d29922;"></div><strong>Yellow background</strong> — Editable assumptions: change for scenarios</div>

  <hr>

  <h2>Key Formulas</h2>
  <table>
    <tr><th>Output</th><th>Logic</th></tr>
    <tr><td>CPI Impact</td><td><code>Oil_Price_Change × Oil_to_CPI_Passthrough</code></td></tr>
    <tr><td>Projected CPI</td><td><code>Baseline_CPI + CPI_Impact</code></td></tr>
    <tr><td>Yield Change</td><td><code>CPI_Impact × Inflation_to_Yield_Beta</code></td></tr>
    <tr><td>GDP Drag</td><td><code>MAX(0, (Oil_Price − 80) × 0.005)</code></td></tr>
    <tr><td>Net Supply Disruption</td><td><code>10 × (1 − Hormuz_Flow%) − OPEC − SPR</code></td></tr>
    <tr><td>Stagflation Score</td><td><code>Inflation_Impact − GDP_Drag</code></td></tr>
  </table>

  <hr>

  <h2>Limitations</h2>
  <div class="warn">
    ⚠️ <strong>Not financial advice.</strong> This is an analytical framework, not a trading signal. Betas are historical estimates and will vary by regime. CME FedWatch and OECD forecasts require manual refresh. UK/German yields are monthly on FRED; use Bloomberg for daily. No VBA/macros — standard Excel formulas, works everywhere.
  </div>

  <hr>

  <h2>Related</h2>
  <p>📝 <strong>Medium Article:</strong> <em>Bonds Are Screaming Two Things at Once — And Both Are Terrifying</em><br>
  📊 <strong>Charts:</strong> 6 original figures (bond yields, oil prices, OECD revisions, tug-of-war diagram, Fed expectations, growth forecasts)<br>
  🌐 <strong>OECD Interim Outlook (Mar 2026):</strong> <a href="https://www.oecd.org/en/publications/oecd-economic-outlook-interim-report-march-2026_d4623013-en.html">oecd.org</a><br>
  📈 <strong>FRED 10Y Yield:</strong> <a href="https://fred.stlouisfed.org/series/DGS10">fred.stlouisfed.org/series/DGS10</a></p>

  <hr>
  <p style="text-align:center; color:#484f58; font-size:13px;">MIT License — use freely, attribution appreciated.</p>

</div>

<script>
function copyMD() {
  const raw = document.getElementById('raw-md').value.trim();
  navigator.clipboard.writeText(raw).then(() => {
    const btn = document.querySelector('.copy-btn');
    btn.textContent = '✅ Copied!';
    btn.classList.add('copied');
    setTimeout(() => {
      btn.textContent = '📋 Copy README.md';
      btn.classList.remove('copied');
    }, 2500);
  });
}
</script>

</body>
</html>
