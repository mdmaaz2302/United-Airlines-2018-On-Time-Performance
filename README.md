# United-Airlines-2018-On-Time-Performance
# UA 2018 Delay Analysis

**Exploratory Data Analysis of United Airlines 2018 on-time performance across 621,565 domestic flights. Uncovers delay patterns by hub, seasonality, and time-of-day. Examines delay causes (Carrier, Weather, NAS, Late Aircraft) and statistical testing. Feature engineering insights for predictive models on delay risk and delay-cause classification.**

---

## 📊 Project Overview

This is an **Exploratory Data Analysis (EDA)** project analyzing United Airlines' 2018 departure delays and cancellations across all domestic flights. The analysis follows the **PACE framework** (Plan, Analyze, Construct, Execute) and provides actionable insights for building predictive delay-risk and delay-cause classification models.

**Dataset:** BTS On-Time Performance data (DOT/RITA)  
**Airlines:** United Airlines (mainline only)  
**Period:** Full year 2018  
**Scope:** 621,565 scheduled domestic flights  
**Hubs Analyzed:** ORD, DEN, IAH, SFO, EWR, LAX, IAD

---

## 📈 Key Findings at a Glance

| Metric | Value | 95% CI |
|--------|-------|---------|
| **Overall Delay Rate** (15+ min) | 17.09% | [17.00%, 17.19%] |
| **Overall Cancellation Rate** | 0.79% | [0.77%, 0.81%] |
| **Avg. Delay** (when delayed) | 74.7 min | — |
| **Hub Effect Size** (Cramér's V) | 0.0786 | Small–moderate |
| **Distance–Delay Correlation** | 0.0075 | Negligible |

**Worst Hub:** EWR (22.84% delay rate)  
**Best Hub:** LAX (11.96% delay rate)  
**Peak Delay Month:** August (24.49%)  
**Peak Cancellation Month:** March (2.23%)

---

## 📁 Contents

### Main Deliverable
- **`UA2018_EDA.ipynb`** – Consolidated Jupyter notebook with 10 sections, embedded charts, and statistical summaries

### Chart Assets (6 visualizations)
1. **`01_delay_rate_by_hub.png`** – Departure delay rate by hub (95% CI bars)
2. **`02_monthly_seasonal_trend.png`** – Dual-axis: delay rate & cancellation rate by month
3. **`03_dow_hour_heatmap.png`** – Delay rate by day-of-week and scheduled departure hour (masked red-eye cells)
4. **`04_delay_cause_by_hub.png`** – Stacked bar: delay-cause composition by hub (Carrier/Weather/NAS/Security/Late Aircraft)
5. **`05_cancellation_rate_by_month.png`** – Cancellation rate trends month-by-month
6. **`06_distance_vs_delay.png`** – Flight distance (buckets) vs. average departure delay (negligible correlation)

### Summary Data
- **`eda_summary.txt`** – Raw statistics tables (hub stats, monthly stats, distance buckets)

---

## 🔍 Analysis Sections

### 1. **Methodology**
- Delay definition: DEP_DELAY ≥ 15 minutes (FAA/DOT standard)
- Hub scope: 7 largest UA airports by 2018 volume
- Confidence intervals: Wilson score method (95%), more reliable for proportions

### 2. **System-Wide KPIs**
- 621,565 flights across 116 origin airports
- 17.09% delay rate with tight 95% CI [17.00%, 17.19%]
- Only 0.79% cancellation rate

### 3. **Hub Effect Analysis** ✅
| Hub | Flights | Delay Rate | 95% CI | Avg Delay (min) |
|-----|---------|-----------|--------|-----------------|
| **EWR** | 58,321 | 22.84% | [22.50%, 23.18%] | 15.19 |
| **ORD** | 77,418 | 20.02% | [19.74%, 20.30%] | 12.32 |
| **SFO** | 60,485 | 19.44% | [19.13%, 19.76%] | 10.49 |
| **IAH** | 61,376 | 17.66% | [17.36%, 17.97%] | 9.54 |
| **DEN** | 63,204 | 15.80% | [15.52%, 16.09%] | 8.53 |
| **IAD** | 25,624 | 14.46% | [14.03%, 14.90%] | 9.22 |
| **LAX** | 28,774 | 11.96% | [11.59%, 12.34%] | 4.74 |

**Chi-Square Test:** χ² = 2318.8, p < 0.001  
**Cramér's V = 0.0786** (small–moderate effect)  
→ Hub is a statistically real predictor, but modest effect size; accounts for only a small portion of delay variance

### 4. **Monthly Seasonality** 📅
- **Winter peaks:** Jan (13.58%), Mar (13.44%) — driven by weather cancellations
- **Summer peak:** Aug (24.49%) — highest delay rate of the year
- **Cancellation separation:** Winter months (Jan/Mar) cancel more than they delay; summer congestion delays more than it cancels

### 5. **Time-of-Day Pattern** ⏰
- **Strong intraday effect:** Delay rate rises steadily through the day
- **Peak hours:** 18:00–21:00 (evening) across all days of week
- **Early morning:** Lowest delays at 04:00–06:00
- **Data quality:** Red-eye slots (02:00–04:59) with <30 flights suppressed to avoid spurious 100% rates

### 6. **Delay-Cause Composition** 🔴
Among delayed flights:
- **Late Aircraft** & **Carrier** dominate at all hubs
- **NAS (system) delay:** Secondary contributor (20–60%)
- **Weather:** Hub-dependent (10–40% of delay minutes)
- **Security:** Negligible (<1%)

### 7. **Cancellation Seasonality** 📵
- **Winter weather:** Jan (1.98%), Mar (2.23%) — highest cancellation rates
- **Summer congestion:** Aug (1.29%) — secondary peak
- **Separation from delays:** Cancellation and delay drivers are distinct → need separate feature emphasis

### 8. **Distance vs. Delay** 📍
| Distance Bucket | Flights | Avg Delay (min) | Delay Rate |
|-----------------|---------|-----------------|-----------|
| <250 mi | 37,339 | 10.44 | 17.18% |
| 250–500 mi | 76,799 | 9.51 | 16.92% |
| 500–750 mi | 89,034 | 10.85 | 17.98% |
| 750–1000 mi | 118,257 | 8.79 | 15.84% |
| 1000–1500 mi | 112,173 | 9.68 | 16.68% |
| 1500–2000 mi | 86,871 | 11.26 | 18.30% |
| 2000–3000 mi | 94,302 | 10.64 | 17.50% |
| 3000+ mi | 6,790 | 8.89 | 14.71% |

**System-wide correlation:** r = 0.0075 (p = 3.48e-09) — statistically significant only due to large *n*, **practically negligible**

**Per-hub test** (Simpson's paradox check): No hub shows meaningful opposite-signed relationship

→ **Conclusion:** Flight distance is NOT a useful delay predictor on its own

---

## 🎯 Feature Engineering Insights

✅ **Keep these features:**
- **Hour of day** – Strong signal; delay rate climbs through day, peaks evening
- **Month/Season** – Clear bimodal pattern (winter cancellations, summer delays)
- **Hub (ORIGIN)** – Statistically real (p < 0.001), modest effect (Cramér's V = 0.079)

⚠️ **Deprioritize/Drop:**
- **Flight distance** – Near-zero correlation (r = 0.0075) system-wide and per-hub

🔀 **Separate modeling:**
- **Delay rate vs. Cancellation rate** have different drivers (congestion vs. weather)
- Consider separate target variables and/or different feature weights for each model

---

## 🛠️ Technology & Libraries

- **Python 3.11+**
- **Jupyter Notebook** – Interactive analysis
- **pandas** – Data manipulation & aggregation
- **matplotlib / seaborn** – Visualization
- **scipy.stats** – Statistical testing (chi-square, correlation)
- **numpy** – Numerical operations
- **nbformat** – Notebook building

---

## 🚀 How to Use

### Option 1: View on GitHub / JupyterLab
1. Clone or download this repo
2. Open `UA2018_EDA.ipynb` in Jupyter
3. All charts and tables are embedded (no external dependencies)

### Option 2: Export to HTML
```bash
jupyter nbconvert --to html UA2018_EDA.ipynb
open UA2018_EDA.html  # View in browser
```

### Option 3: Use for Feature Engineering Reference
- Reference the **Feature Engineering Insights** section above
- Use hub-level delay rates and delay-cause profiles as baseline for modeling
- Check per-hub correlations before feature selection

---

## 📊 Data Source

**United Airlines 2018 On-Time Performance**
- **Source:** Bureau of Transportation Statistics (BTS), DOT/RITA
- **Download:** https://www.transtats.bts.gov/
- **Dataset:** On-Time Performance data, domestic flights only
- **Rows:** 621,565 scheduled departures
- **Columns:** Origin, destination, scheduled/actual departure/arrival, delay minutes, delay cause (categorical)

---

## 📋 Next Steps / Future Work

1. **Predictive Modeling** – Random Forest + Logistic Regression for:
   - Model A: Delayed (Y/N) / Cancelled (Y/N) prediction from pre-flight-known features
   - Model B: Delay cause classification (Carrier, Weather, NAS, Security, Late Aircraft) among already-delayed flights

2. **Leakage-Safe Feature Engineering**
   - Exclude realized delay causes, realized actual times
   - Use only scheduled info, historical hub/month/hour patterns

3. **Model Validation**
   - Cross-validation with time-based splits (respect temporal order)
   - Test on held-out 2019 data (if available) for external validity

4. **Deployment**
   - Build delay-risk scoring API for booking/operations
   - Integrate delay-cause predictions into customer communications

5. **Enhanced Seasonality**
   - Investigate specific weather events (winter storms, summer heat waves)
   - Correlate with external weather data (temperature, precipitation, wind)

---

## 👤 Author

**MD Maaz** ([@mdmaaz2302](https://github.com/mdmaaz2302))  
Data Science Portfolio Project  
*Building toward F1 data science career*

---

## 📄 License

This project is for educational and portfolio purposes. Data source: U.S. Department of Transportation.

---

## 📞 Questions or Feedback?

- **GitHub Issues:** Open an issue for questions or suggestions
- **LinkedIn:** [linkedin.com/in/mdmaaz2302](https://linkedin.com/in/mdmaaz2302)
- **Portfolio:** [github.com/mdmaaz2302](https://github.com/mdmaaz2302)

---

## 🎓 Project Methodology (PACE Framework)

### **Plan**
- Define analysis scope: UA 2018 domestic flights, 7 major hubs
- Identify key questions: hub effects, seasonality, delay causes, distance correlation
- Select statistical methods: chi-square, correlation, confidence intervals

### **Analyze**
- Aggregate delay/cancellation rates by hub, month, day–hour, distance
- Run statistical tests to validate significance
- Check for confounding variables (e.g., Simpson's paradox)

### **Construct**
- Build EDA dashboards and summary tables
- Embed visualizations and metadata
- Document methodology and limitations

### **Execute**
- Package findings in reproducible Jupyter notebook
- Present actionable insights for downstream modeling
- Create feature engineering roadmap

---

*Last updated: August 2026*
