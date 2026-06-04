# LAX Flight Delay Analysis — Power BI Dashboard

An exploratory analysis of flight delay patterns at Los Angeles International Airport (LAX), built in Power BI as the capstone project of my Business Intelligence & Data Analytics Weiterbildung at Stackfuel Berlin (2025). The project is in German.

The analysis covers **2015–2017** and focuses on three questions:
- Which airlines have the highest delay rates and highest average delay per flight at LAX?
- In which time periods are flights most frequently delayed — by year, quarter, month, calendar week, weekday, and hour of day?
- What recurring patterns emerge, and what operational conclusions can be drawn?

> **Definition used:** A flight is classified as delayed if it departs or arrives 5+ minutes off schedule (early or late). Cancelled and diverted flights are excluded.

---

## Dashboard structure

| Page | Content | Preview |
|---|---|---|
| Intro | Project brief and research questions |
| Overview air traffic | KPI overview — 1.264.229 total flights, 70.2% delay rate, avg. 26.42 min delay | ![Overview](1_LAX_overview-air-traffic.png) |
| Overview Airlines | Airline market share at LAX (top 5 account for 80%+) |
| Top 3 Airlines | Airlines by avg delay per flight and delay share | ![Top 3 Airlines](2_LAX_top-3-airlines.png) |
| Timeframe — year/quartal/month | Delay trends by year, quarter, and month | ![Timeframe](3_LAX_timeframe.png) |
| Timeframe — KW | Delay trends by calendar week, with event annotations |
| Timeframe — day | Delay rate by day of week |
| Timeframe — hour | Delay rate by hour of day |
| Punctuality distribution | Delay distribution | ![Punctuality Distribution](4_LAX_punctuality-distribution.png) |
| Findings | Results and operational recommendations | ![Findings](5_LAX_findings.png) |
| Datenset | Raw data view |

---

## Key findings

**Airlines**
- The four airlines with the highest share of delayed flights are **Southwest Airlines**, **American Airlines**, **SkyWest Airlines**, and **Delta Air Lines** — which together also account for the majority of total traffic at LAX
- The analysis distinguishes between *share* of delayed flights (volume) and *average delay per flight* (severity), which do not always rank airlines in the same order

**Temporal patterns**
- Delays increased sharply in **2017** compared to 2015–2016
- **Q1 is consistently the worst quarter** for delays across all three years
- **December is the worst individual month**
- At calendar week level, delay spikes cluster around **KW 1 (New Year)**, **KW 10 (US Daylight Saving Time change)**, and **KW 52 (Christmas)**
- **Sundays and evening hours** show the highest delay rates by day and time of day
- **2:00–4:00 AM** shows disproportionately high delay rates despite very low flight volume — likely linked to maintenance windows or night-operation constraints

**Operational conclusions** (from Erkenntnisse page)
- LAX can most efficiently improve overall punctuality by targeting cooperation and process measures with the four high-volume airlines above
- Slot planning and additional ground resources should be evaluated specifically for Q1, December, KW 1/10/52, Sundays, and evening peaks
- Distribution analysis shows that a large share of early arrivals/departures fall within moderate deviations — average delay alone understates the pattern; percentile measures (P2.5, P97.5) were included to capture this

---

## DAX measures built

| Measure | Description |
|---|---|
| `tot_flights` | Total flight count |
| `delayed_flights` | Count of flights meeting the 5-min delay threshold |
| `delay_rate` | Share of delayed flights (%) |
| `avg_delay` | Average delay in minutes per flight |
| `highest_day` | Day with peak delay rate |
| `Percentile_025` / `Percentile_975` | Distribution spread (P2.5 and P97.5) |

---

## Data model

The report uses the following fields from the source dataset:

| Field | Description |
|---|---|
| `fl_date` | Flight date |
| `fl_time` / `fl_time_h` / `fl_time_4h` | Departure time at different granularities |
| `fl_date_day` | Day of week |
| `delay_LAX` / `delay_LAX_5-mm` | Delay in minutes / binary delay flag |
| `flight_type` | Departure or arrival |
| `status` | On-time / delayed / early |

---

## Tools & techniques

| Layer | Details |
|---|---|
| **Tool** | Power BI Desktop |
| **Transformation** | Power Query (M) — cleaning, date/time parsing, delay flag calculation |
| **Calculations** | DAX — rate measures, averages, percentiles, time intelligence |
| **Visualisations** | KPI cards, combo charts, bar/column charts, area chart, pie chart, slicers |
| **Data source** | US Bureau of Transportation Statistics (BTS) — Reporting Carrier On-Time Performance dataset |

---

## How to open this project

1. Download [`LT_lax-flight-delay-analysis.pbix`](./LT_lax-flight-delay-analysis.pbix)
2. Open in **Power BI Desktop** (free — [download here](https://powerbi.microsoft.com/desktop/))
3. All data is embedded — no external connection required

> Screenshots coming soon.

---

**[Ludovica Trentini](https://github.com/ludovicatrentini)** · [LinkedIn](https://www.linkedin.com/in/ludovicatrentini) · Berlin
