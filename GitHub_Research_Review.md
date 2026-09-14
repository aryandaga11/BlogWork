**GitHub research review — Aryan Daga**

Reviewed September 14, 2026. Repository: [aryandaga11/BlogWork](https://github.com/aryandaga11/BlogWork), branch `main`, commit `865f6d15d86ef93cf14198a03f8824a3b28d8016`.

**Recommendation: make `macro pitch.xlsx` the active project. Repair its data definitions and connect the economic evidence to market-implied policy pricing. Keep the old inflation workbook and R script as a secondary research exercise.** The existing collection is sufficient to begin a focused memo, but it does not yet establish that Fed policy or Treasury yields are mispriced.

The GitHub connection returned one accessible repository and one branch. All four current files were opened. The review covered all four workbook sheets, populated cells, formulas and cached results, both native chart definitions, the embedded Bloomberg image, and the complete R script and README. Source checks were targeted spot checks, not a complete re-download and reconciliation of every historical observation. No repository files were modified. The R specification was independently replicated with NumPy ordinary least squares; native R execution was unavailable. The benchmarks below are retrospective diagnostics, not a certified real-time forecasting backtest.

| File | Contents | Recommended role | Priority |
|---|---|---|---|
| [macro pitch.xlsx](https://github.com/aryandaga11/BlogWork/blob/865f6d15d86ef93cf14198a03f8824a3b28d8016/macro%20pitch.xlsx) | Market snapshot, 1,423 dated Treasury observations, 68 monthly macro rows, two native charts and a Bloomberg screenshot | Main memo and supporting model | First |
| [USA.xlsx](https://github.com/aryandaga11/BlogWork/blob/865f6d15d86ef93cf14198a03f8824a3b28d8016/USA.xlsx) | 240 monthly observations, January 2004–December 2023; 14 numeric series | Historical reference and model-development dataset after source reconciliation | Second |
| [Inflation Project](https://github.com/aryandaga11/BlogWork/blob/865f6d15d86ef93cf14198a03f8824a3b28d8016/Inflation%20Project) | R exploration, three OLS specifications, flawed train/test evaluation | Learning project requiring a corrected evaluation design | Third |
| [README.md](https://github.com/aryandaga11/BlogWork/blob/865f6d15d86ef93cf14198a03f8824a3b28d8016/README.md) | Short repository description | Navigation and explanation for a professional reader | Quick improvement |

**1. `macro pitch.xlsx`: the strongest starting point**

The useful foundation is already present: a daily 2-year/10-year history, a calculated curve spread, monthly inflation and labor data, a policy snapshot, and an initial comparison of the 2-year yield with the Fed target. The missing step is a dated, sourced comparison between your conditional policy view and the policy path embedded in prices.

**The `Sheet1` snapshot**

Cells `B3:F4` contain manually entered Treasury yields. `B6:F6` correctly calculate 10-year minus 2-year spreads in basis points using `=(B3-B4)*10000` and its copied equivalents. Those yields are stored as decimal fractions, so the multiplier is correct. The displayed current spread of 41.7 bp reconciles to the stored 4.789% and 4.372% yields.

The main weaknesses are dates, source traceability, and independent manual inputs:

| Location | Finding | Work to do |
|---|---|---|
| `A2` | Text label says `DATE: 09/07/26`; the daily history continues through September 10 | Use a real as-of date and identify the observation date/time and source behind each quote. September 7 has no FRED DGS2/DGS10 observation. A carried or alternative-source quote needs that explanation. |
| `B2:F2` | “Current,” “5 Days,” “1 Month,” “3 Months,” and “YTD” do not identify exact historical dates | State whether these mean prior trading-day levels, calendar lookbacks, averages, or changes. Show the comparison dates. |
| `B3:F4` | Snapshot values do not link to the daily source sheet | Link to the selected history where definitions match. If Bloomberg generic yields are intentional, retain them with their ticker, timestamp and quote convention. |
| `B9:F10` | FOMC target ranges and vote counts sit underneath Treasury lookback headings | Give FOMC decisions a separate meeting-date table. |
| `B9:F9` | Target ranges are text strings | Keep numeric lower bound, upper bound and midpoint if they will feed calculations. Distinguish all three from the effective federal funds rate. |

The vote counts themselves match the five completed 2026 meetings in reverse chronological order. This is primarily a labeling problem, and the dissent direction adds useful information:

| Current cell | Correct meeting date | Vote | What the dissent meant |
|---|---|---|---|
| `B10` | July 29, 2026 | 9–3 | Three preferred a 25 bp increase. [Fed statement](https://www.federalreserve.gov/newsevents/pressreleases/monetary20260729a.htm) |
| `C10` | June 17, 2026 | 12–0 | Unanimous. [Fed statement](https://www.federalreserve.gov/newsevents/pressreleases/monetary20260617a.htm) |
| `D10` | April 29, 2026 | 8–4 | One preferred a cut; three supported holding rates but opposed the statement’s easing bias. [Fed statement](https://www.federalreserve.gov/newsevents/pressreleases/monetary20260429a.htm) |
| `E10` | March 18, 2026 | 11–1 | One preferred a 25 bp cut. [Fed statement](https://www.federalreserve.gov/newsevents/pressreleases/monetary20260318a.htm) |
| `F10` | January 28, 2026 | 10–2 | Two preferred a 25 bp cut. [Fed statement](https://www.federalreserve.gov/newsevents/pressreleases/monetary20260128a.htm) |

All five statements maintained a 3.50–3.75% target range. A vote split alone would conceal the shift in the direction of disagreement. Add one sentence on the rationale and links to the statement, minutes and projections when available.

**The `2s & 10s` history and charts**

The usable history occupies `A2:C1424`: January 4, 2021–September 10, 2026. Dates are sorted and unique, and both yield columns are populated for all 1,423 dated rows. The valid-row spread formulas and saved results reconcile. Here yields are stored as percentage-point numbers such as `4.95`, so `=(B2-C2)*100` is correct. The different multiplier from `Sheet1` reflects different storage conventions, not a mathematical error.

There is one confirmed false observation: `D1425` contains `=(B1425-C1425)*100`, while `A1425:C1425` are blank. Excel treats the blank inputs as zero, producing a fictitious zero spread. `Table1` and both chart ranges extend through row 1425. Restrict them to actual observations and make future spread calculations require a valid date and two numeric yields. The source chart includes the unwanted row; its exact visual effect depends on chart handling of the blank date.

The spread chart also has its date axis disabled in the original chart XML and no explicit title. Restore a visible date axis and title such as “10-year minus 2-year Treasury yield, basis points.” The yield chart has series labels. Its axes are enabled in the source, although the preview renderer did not display them faithfully, so a native Excel check is appropriate before exporting publication charts. A stray `x` is present at `W21` and can be removed during cleanup.

The latest dated source row is 10-year **4.95%**, 2-year **4.56%**, spread **39 bp**. Those yields match the latest observations returned by FRED during this review. From September 4 to September 10, the workbook shows the 10-year rising 17 bp and the 2-year rising 19 bp: a small bear flattening. This describes the move; it does not explain its cause. [FRED DGS10](https://fred.stlouisfed.org/series/DGS10), [FRED DGS2](https://fred.stlouisfed.org/series/DGS2).

Monthly averages are appropriate for a descriptive comparison with monthly macro data. Preserve daily observations for a pricing snapshot or event study. Calculate a monthly spread using matched observation dates; exclude the blank row. Month-end levels and monthly averages answer different questions, so label them separately. A change in yield belongs in basis points, not a percentage change in the yield itself.

**The embedded Bloomberg screenshot**

The image compares `USGG2YR Index` with `FDTR Index`, identified in the image as the federal funds target upper bound. The displayed difference is about **66.48 bp**. It is a 2-year-versus-policy-rate comparison, not the 2s10s spread. The screenshot’s end-date field is September 9, 2026, but an exact quote timestamp and exported underlying data are absent.

This is a useful candidate exhibit for the research question. A 2-year yield above today’s policy rate can reflect expectations for the future short-rate path and risk compensation. It does not, by itself, establish that the Fed is behind the curve or that the Treasury is cheap. Add the market-implied policy path, use consistent quote times, and explain why the upper bound is the selected comparator rather than the midpoint or effective rate.

**The `Macro Data` sheet**

There are 68 consecutive monthly date rows from January 2021 through August 2026 and eight series. Dates are sorted, unique and stored as actual Excel dates. There are no calculation formulas on this sheet. Except for three text `N/A` entries and two blank latest observations, all eight series contain numeric values.

The priority is the **apparent PPI definition splice at January 2023**. The new workbook exactly matches the old workbook’s PPI for all 24 months of 2021–2022, then differs in every month of 2023:

| Month | `USA.xlsx`, PPI | `macro pitch.xlsx`, PPI | New-workbook cell |
|---|---:|---:|---|
| February 2023 | 2.4% | 4.7% | `G27` |
| March 2023 | −1.1% | 2.7% | `G28` |
| June 2023 | −9.4% | 0.3% | `G31` |
| December 2023 | −3.1% | 1.1% | `G37` |

The later numbers are consistent with year-over-year growth in the seasonally adjusted final-demand PPI series `PPIFIS`. For example, its June 2022 and June 2023 levels are 140.273 and 140.698, implying about 0.303%. Its January 2023 calculation rounds to 5.7%, matching `G26`. The earlier block appears to use a broader commodity-price measure. That identification is an inference from the values and overlap, since neither workbook provides its original series IDs. **Do not model or publish the combined PPI column until one definition is verified across the entire history.** For this pitch, a consistently sourced final-demand PPI is a reasonable choice; an all-commodities measure can remain a separately named energy/input-cost series if useful. [FRED final-demand PPI data](https://fred.stlouisfed.org/data/PPIFIS), [FRED all-commodities PPI definition](https://fred.stlouisfed.org/series/PPIACO).

Other cross-file differences over the 36 overlapping months deserve reconciliation:

| Shared series | Differing observations | Interpretation |
|---|---:|---|
| CPI / Inflation | 0 of 36 | The overlapping values agree. |
| InterestRates | 0 of 36 | The overlapping values agree. |
| UnemploymentRate | 1 of 36 | December 2023 is 3.8% in the new workbook versus 3.7% in the old one. Check vintage/revision. |
| RetailTrade | 35 of 36 | Revisions or a different retail aggregate are plausible. Exact series and retrieval date are required. |
| PPI | 12 of 36 | All mismatches occur in 2023; likely a definition change. |
| WageGrowth | 21 of 36 | Verify source vintage, population and any smoothing. Do not silently join the histories. |

Differences are not automatically transcription mistakes. Current revised data and historical releases can legitimately disagree.

The missing-data treatment is largely sensible:

- `B59`, `E59` and `H59` contain text `N/A` for October 2025 CPI, unemployment and wage growth. BLS did not publish October all-items CPI and did not collect the household survey; the Atlanta Fed also identifies a missing October wage-growth observation. Keep the gap and document the reason. Do not turn it into zero or interpolate it as an observed fact. [BLS explanation](https://www.bls.gov/bls/2025-lapse-revised-release-dates.htm), [Atlanta Fed Wage Growth Tracker](https://www.atlantafed.org/research-and-data/data/wage-growth-tracker).
- `C69` and `F69`, August 2026 PCE and retail trade, are blank. They should remain explicitly unavailable unless verified releases can fill them. The differing publication schedules mean the latest usable observation is not the same for every series.
- `G66:G69` retain preliminary-data notes. Preserve those notes and record retrieval dates when refreshing.

The last five values in `5Y BREAK` match FRED’s monthly `T5YIEM` series, including July and August 2026 at 2.26%. Rename the column to state the maturity and monthly convention. Keep a daily breakeven series for event and current-pricing work. Breakevens incorporate inflation expectations, inflation risk compensation and liquidity effects; they are not a pure inflation forecast and do not share the same horizon as current year-over-year CPI. [FRED monthly 5-year breakeven](https://fred.stlouisfed.org/series/T5YIEM), [Federal Reserve discussion of TIPS compensation](https://www.federalreserve.gov/econres/notes/feds-notes/tips-from-tips-update-and-discussions-20190521.html).

Add a compact definition register: exact source/series ID, units, seasonal adjustment, transformation, aggregation, observation period, release date and retrieval date. The date `2026-08-01` denotes an August reference month, not availability on August 1. This distinction is essential when judging what the Fed or market could have known at a particular meeting.

**2. `USA.xlsx`: useful historical material, with unresolved provenance**

The single `usa` sheet has 240 consecutive monthly dates from January 2004 through December 2023. All 14 numeric columns are populated. No duplicate dates or missing calendar months were found. There are no formulas, charts, source hyperlinks or explanatory notes. Its clean rectangular structure is a strength, but complete cells do not establish correct economic definitions.

| Columns | Useful purpose | Verification or transformation needed |
|---|---|---|
| `Inflation`, `Food`, `Energy` | Aggregate and component inflation history | Confirm exact CPI baskets, year-over-year convention and seasonal treatment. Component inflation rates are not additive contributions. |
| `InterestRates` | Historical policy conditions | Values are consistent with an effective-fed-funds-style series; verify the ID. Distinguish effective rate from target bounds. |
| `UnemploymentRate` | Labor-market context | Confirm seasonal treatment and data vintage, including the December 2023 discrepancy. |
| `RetailTrade` | Consumer-demand proxy | Define the aggregate and nominal/real treatment. Values resemble monthly growth, unlike the annual inflation measures. |
| `PPI`, `FPPI`, `EPPI` | Producer-price and input-cost channels | Specify the baskets and annual/monthly transformations. These labels are insufficient for a defensible model. |
| `WageGrowth` | Wage-pressure context | Verify whether this is the Atlanta Fed tracker and which unsmoothed/smoothed variant. |
| `FoodSectorWages`, `ManuSectorWages` | Possible sector labor-cost evidence | Highest definition uncertainty. Verify nominal versus real, hourly versus weekly, population and original frequency before interpreting coefficients. |
| `WheatPrices`, `WTI` | Commodity-price channels | State currency, units, benchmark and monthly aggregation. For annual component inflation, annual commodity-price changes are often a more coherent starting specification than nominal price levels. |

`FoodSectorWages`, for example, is −1.8 in January 2004 and −5.0 in April 2020. These values are not proof of a mistake, but the name does not explain whether this is a wage measure, real earnings, growth, or another labor statistic. Quarantine it from interpretation until its source is recovered.

Preserve this file as a historical snapshot. Do not automatically append its columns to the new workbook or spend the next work session extending every series. Recover the definitions needed for the current pitch first. It is a historical reference rather than a current-market dataset, since it ends in 2023.

**3. `Inflation Project`: sound exploratory ingredients, unreliable evaluation**

The script imports the old workbook, draws time-series and scatter plots, and estimates three regressions: headline inflation on five macro variables; food inflation on food PPI, wheat, sector wages and rates; and energy inflation on WTI. Its component-based thinking is useful. The evaluation design does not support predictive claims.

| Location in original script | Issue | Consequence and correction |
|---|---|---|
| Line 83 | `Model_One` uses `data = USA` after a train/test split has been created | Every supposed test observation was included in estimation. Fit on the training subset only. |
| Line 76 | Randomly samples monthly observations | Future regimes leak into training for a forecasting exercise. Use an ordered split or expanding-window evaluation. A random seed would make the flawed experiment repeatable but would not fix it. |
| Lines 83–87 | Uses contemporaneous macro inputs with no forecast horizon or release calendar | Even a chronological split is not a real-time forecast when the period’s predictors were not known at the forecast origin. Define a target horizon and use available lagged inputs or explicitly call the exercise explanatory. |
| Line 103 | Calls squared actual/predicted correlation test R-squared | This can hide level and scale errors. Report MAE/RMSE and a clearly defined SSE-based or benchmark-relative score. |
| Lines 64–72 | Contemporaneous regressions are vulnerable to joint responses, reverse causality and persistent residuals | A positive rates coefficient does not demonstrate that higher rates cause inflation. Avoid causal language without identification. |
| Line 71 | Regresses an apparent annual energy-inflation rate on the WTI price level | Inspect annual WTI changes and lagged transmission as a diagnostic alternative, then validate separately. |
| Line 2 | Uses a machine-specific working-directory-dependent path | Rename the file with `.R` and use a documented project-relative data path. |
| Lines 3, 39, repeated plot/model blocks | Interactive `View()`, “Simulated Phillips Curve” on observed data, duplicated headline model, no saved results | Make batch execution explicit, correct the label, keep one model definition and save figures/results. |

The date conversion is not a demonstrated bug: the workbook contains real Excel dates. Validate the imported type rather than assuming the formatting string means the dates are broken. Similarly, MAE and RMSE are correctly written for complete finite predictions; missing-value handling needs an explicit policy if the data expand.

Independent replication of the original full-sample specifications produced:

| Original specification | Observations | In-sample R² | RMSE, percentage points | Lag-1 residual correlation |
|---|---:|---:|---:|---:|
| Headline inflation, five predictors | 240 | 0.882 | 0.666 | 0.785 |
| Food inflation, four predictors | 240 | 0.599 | 1.498 | 0.950 |
| Energy inflation on WTI level | 240 | 0.184 | 12.421 | 0.934 |

These are fits to the supplied data, not forecasting achievements. The residual persistence is a reason to reconsider dynamics and ordinary OLS inference.

A separate diagnostic uses January 2004–December 2019 as the first 192 training observations, then evaluates January 2020–December 2023, the last 48 observations:

| Evaluation on the same 48 months | RMSE, percentage points | SSE-based R² |
|---|---:|---:|
| Original specification fitted on all 240 months, including these 48 | 0.906 | 0.885 |
| Original specification fitted only on 2004–2019; realized contemporaneous predictors supplied for 2020–2023 | 1.928 | 0.479 |
| Previous month’s inflation used for the current month | 0.549 | 0.958 |

The chronological model still receives realized current-period predictors, which is favorable relative to a real forecasting problem. Despite that, it underperforms a simple one-month persistence benchmark. The pandemic-heavy holdout is demanding, so this is evidence of a validation problem and regime sensitivity, not proof that every future version must fail. The test is also one-month-oriented; it does not establish performance at the pitch’s 3–12 month horizon.

The metric issue is material: on that chronological evaluation, squared prediction correlation is about **0.739**, while SSE-based R² is **0.479**. The correlation measure gives a substantially more flattering impression. The wage coefficient also changes from approximately **0.091** in the pre-2020 fit to **0.775** in the full sample, illustrating sensitivity to the included regime.

For the energy model, on the same 228 usable observations after constructing annual oil changes, replacing the WTI level with WTI year-over-year percentage change raises in-sample R² from **0.234** to **0.687**. This is a useful transformation check, not an endorsed forecasting model. Low oil-price base effects, lags and energy-component composition still matter.

Recommended minimum repair if returning to this script: recover definitions, choose explanatory versus predictive purpose, define a horizon, train only on past data, use information available at each forecast origin, compare with a persistence benchmark at the same horizon, and save the results. An extensive new model is unnecessary for the first memo.

**4. `README.md`: make the work understandable to someone opening the repository**

The current README is a 111-byte general description. It does not state the research question, explain which work is current, map the files, provide execution instructions, link a memo, or disclose the model’s limitations.

A short replacement should contain the exact research question; the intended 3–12 month horizon; a file index; a link to the current memo and workbook; source/update conventions; basic R dependencies (`readxl`, `ggplot2`); and an honest status note that the old regression is exploratory and its validation is being corrected. The most useful presentation upgrade is one finished research conclusion with supporting charts. Repository cosmetics can follow.

**Recommended work order**

| Order | Work | Concrete result | Suggested effort |
|---|---|---|---|
| 1 | Repair and define the current workbook | Consistent PPI history; dated FOMC table; valid Treasury ranges; source/units register; one as-of convention | 2–3 hours |
| 2 | Add the missing pricing evidence | Dated policy path at roughly 3, 6 and 12 months; matched 10-year nominal yield, real yield and breakeven; term-premium estimate if available | 2–3 hours |
| 3 | Add only decision-relevant economic context | Core PCE momentum, a measure of employment growth, and real activity/consumption; a small risk-to-market transmission table | 2–3 hours |
| 4 | State the disagreement and write | Three conditional cases with Fed response, 2-year/10-year implications, catalysts and invalidation; a 1,000–1,500 word memo | 3–5 hours |
| 5 | Package the evidence | Three or four clear charts, refreshed README and saved source dates | About 1 hour |

Effort figures are planning estimates. They keep the first package within the intended modest scope. The old script can be revisited afterward as a separate improvement exercise.

The essential missing market input is a **forward policy path**. Today’s effective rate, the target range and the 2-year yield are different objects. Capture OIS or rate-futures-implied policy expectations at a common timestamp using available market data. CME FedWatch is a public alternative for meeting probabilities derived from fed-funds futures; record its assumptions and do not treat those probabilities as an unbiased forecast. [CME FedWatch](https://www.cmegroup.com/markets/interest-rates/cme-fedwatch-tool.html).

For the 10-year, use matched-maturity nominal and real yields and a 10-year breakeven to examine the nominal/real/inflation-compensation relationship. Keep the existing 5-year breakeven as its own horizon. A term-premium estimate offers a different decomposition of nominal yields into an expected-rate component and term compensation. Do not add the real yield, breakeven and a nominal term-premium estimate together: that double counts components. Label term-premium estimates as model-dependent.

Add core PCE price levels or properly sourced short-horizon growth rates to evaluate momentum. Do not annualize a three-month average of year-over-year rates and call it three-month inflation. From a monthly price index, the three-month annualized calculation is `100*((P_t/P_(t-3))^4-1)`. Keep headline inflation for the household and energy shock, and core inflation for persistence; both can matter for policy.

For geopolitics and domestic risks, choose two or three mechanisms with observable evidence. For each, specify: shock, transmission into US inflation/growth, plausible Fed response, what market prices already reflect, and the evidence that would invalidate the view. Energy disruption could lift headline inflation but also weaken real demand; that does not force one Treasury reaction across every horizon.

The scenario table should be compact:

| Conditional case | Evidence to monitor | Policy view versus pricing | Market implication to articulate |
|---|---|---|---|
| Inflation persists and activity holds | Core inflation momentum, employment and demand | Is the priced path sufficiently restrictive? | Specify separate 2-year and 10-year responses and why. |
| Supply shock fades and inflation slows | Energy pass-through, core trend and expectations | Does the market price enough or too much easing? | Explain which maturity benefits and what could offset it. |
| Growth deteriorates while inflation remains uncomfortable | Jobs, real spending, credit conditions | How does the dual-mandate tradeoff change the path? | Separate front-end easing expectations from long-end inflation/term compensation. |

No probabilities or precise yield targets need to be invented before the evidence supports them. A conditional memo can still be differentiated if it states where the market’s implied path seems vulnerable, what would trigger repricing, and what would prove the argument wrong.

**The next work session should end with a repaired PPI definition, an explicitly dated market snapshot, a meeting-date FOMC table, and a short paragraph stating the particular policy/pricing disagreement to investigate.** Those items will move this collection toward a publishable macro argument faster than expanding the old regression.
