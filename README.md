
# 🛡️ GigShield — AI-Powered Parametric Income Insurance for India's Gig Economy

> **Guidewire DEVTrails 2026 | University Hackathon Submission**  
> Protecting India's Q-Commerce delivery partners from income loss caused by uncontrollable external disruptions.

---

## 📌 Table of Contents

- [Problem Statement](#-problem-statement)
- [Our Solution](#-our-solution)
- [Persona & Scenarios](#-persona--scenarios)
- [Application Workflow](#-application-workflow)
- [Weekly Premium Model](#-weekly-premium-model)
- [Parametric Triggers](#-parametric-triggers)
- [AI/ML Integration](#-aiml-integration)
- [Fraud Detection Architecture](#-fraud-detection-architecture)
- [Platform Choice & Justification](#-platform-choice--justification)
- [Tech Stack](#-tech-stack)
- [Development Plan](#-development-plan)
- [Team](#-team)

---

## 🚨 Problem Statement

India's Q-Commerce delivery partners (Zepto, Blinkit, Swiggy Instamart) operate in hyper-dense urban micro-zones with 10-minute delivery windows. External disruptions — heavy rain, extreme heat, local curfews, zone floods — can wipe out 20–30% of their weekly earnings in a single day.

**Current reality:**
- No existing income protection product for gig workers
- Traditional insurance requires manual claims, which workers cannot navigate
- Disruptions are objective and verifiable — yet no automated safety net exists
- Workers live week-to-week with zero financial buffer

**Coverage strictly limited to:** Loss of income due to external parametric events only.  
**Explicitly excluded:** Health, life, accidents, vehicle repairs.

---

## 💡 Our Solution

**GigShield** is a zero-touch, AI-enabled parametric income insurance platform built exclusively for Q-Commerce delivery partners. 

The core innovation: **workers never file a claim.**

When a verified disruption occurs in a worker's registered delivery zone, GigShield's trigger engine detects it automatically, cross-validates the worker's inactivity via GPS, and initiates payout — all within 5 minutes. The worker receives a WhatsApp/SMS notification:

> *"Heavy rain detected in Koramangala Zone 4. ₹220 has been credited to your UPI wallet."*

No forms. No uploads. No waiting.

---

## 👤 Persona & Scenarios

### Chosen Persona: Q-Commerce Delivery Partner (Zepto / Blinkit)

**Why Q-Commerce?**
- Operate within fixed 2km dark-store zones — highly localized disruption exposure
- Earn per-order, not per-hour — income loss is immediate and measurable
- Predominantly young, smartphone-native — ideal for a digital-first product
- Most vulnerable to hyperlocal weather events (a flooded street = entire zone offline)

---

### Scenario 1 — Ravi, Mumbai (Monsoon Shutdown)

Ravi is a Zepto delivery partner operating out of the Andheri West dark store. On a Tuesday evening, Mumbai receives 48mm of rainfall in 2 hours. Zone-level order volume drops by 72%. Ravi is marked as "online but inactive" in Zepto's system for 3.5 hours.

**GigShield Response:**
1. IMD weather API reports >20mm/hr rainfall in Ravi's registered zone.
2. Trigger Engine fires `TRIGGER_HEAVY_RAIN`.
3. Fraud Guard cross-checks: GPS confirms Ravi is in zone, order volume confirms drop, no active deliveries detected.
4. Payout calculated: 3.5 hrs × ₹65 avg. hourly earning = **₹227 credited in 4 minutes**.

---

### Scenario 2 — Priya, Delhi (Heat Wave)

Priya delivers for Blinkit in West Delhi. At 1:30pm in May, the temperature hits 44°C. Delhi's heat action plan restricts outdoor work for 3 hours (12–3pm). Priya is unable to work her peak lunch slot.

**GigShield Response:**
1. IMD reports temperature >42°C sustained for >1 hour in Priya's zone.
2. Trigger Engine fires `TRIGGER_EXTREME_HEAT` (midday window only).
3. Payout: 2.5 covered hours × ₹58 avg. = **₹145 credited automatically**.

---

### Scenario 3 — Arun, Chennai (Zone Curfew)

Arun operates from a Zepto dark store in T. Nagar. An unexpected local strike blocks all vehicle movement in the zone for 6 hours. Arun cannot reach the store or complete any deliveries.

**GigShield Response:**
1. Verified strike notification detected via government alert API + news scraper.
2. GPS confirms Arun is blocked outside the zone perimeter.
3. Full 6-hour shift covered. Payout = **₹390 credited via UPI**.

---

## 🔄 Application Workflow

```
┌─────────────────────────────────────────────────────────────────┐
│                        WORKER JOURNEY                           │
│                                                                 │
│  [Onboarding] → [Zone Registration] → [Weekly Plan Selection]  │
│       ↓                                                         │
│  [Coverage Active] ←── Monday auto-renewal prompt              │
│       ↓                                                         │
│  [Disruption Occurs] ← External event in worker's zone         │
│       ↓                                                         │
│  [Auto Detection] ← Trigger Engine + GPS validation            │
│       ↓                                                         │
│  [Fraud Check] ← 3-signal cross-validation (AI)                │
│       ↓                                                         │
│  [Auto Payout] → UPI / wallet in < 5 minutes                   │
│       ↓                                                         │
│  [Notification] → WhatsApp + in-app summary                    │
└─────────────────────────────────────────────────────────────────┘
```

### Onboarding (< 3 minutes)
1. Worker downloads the GigShield PWA or opens the WhatsApp bot
2. Enters mobile number → verified via OTP
3. Links delivery platform account (Zepto/Blinkit partner ID)
4. Selects registered delivery zone (auto-suggested from GPS)
5. AI Risk Engine computes their zone's weekly risk score
6. Worker sees personalised weekly premium and selects a plan

### Weekly Activation
- Every Monday, push notification: *"Your coverage for this week: ₹49. Tap to activate."*
- One-tap UPI autopay or manual confirm
- No activation = no charge, no coverage
- Coverage window: Monday 6am → Sunday 11:59pm

---

## 💰 Weekly Premium Model

All pricing is structured on a **weekly basis** to align with the gig worker earnings cycle.

### Base Plan Tiers

| Plan | Avg Weekly Hours | Weekly Premium | Max Weekly Payout | Covered Events |
|------|-----------------|----------------|-------------------|----------------|
| **Lite** | 20–30 hrs | ₹39 | ₹600 | 2 triggers/week |
| **Standard** | 30–45 hrs | ₹59 | ₹1,000 | 4 triggers/week |
| **Power** | 45+ hrs | ₹89 | ₹1,600 | Unlimited triggers |

### Dynamic Pricing via ML (Zone Risk Adjustment)

The base premium is adjusted weekly using a **Zone Risk Score** computed by our ML model:

```
Final Weekly Premium = Base Premium × (1 + Zone Risk Multiplier) × Seasonal Loading

Zone Risk Multiplier range: -0.15 to +0.25
Seasonal Loading: 1.0 (dry) → 1.3 (peak monsoon)
```

**Zone Risk Score inputs:**
- Historical flood/waterlogging frequency in zone (3-year IMD data)
- Historical curfew/strike frequency (news archive data)
- Average summer peak temperature
- Zone elevation and drainage rating (municipal data)

**Example:** A Standard plan worker in a high-flood zone during monsoon season:  
`₹59 × (1 + 0.20) × 1.25 = ₹88.50/week`

A Standard plan worker in a historically safe zone in winter:  
`₹59 × (1 - 0.10) × 1.0 = ₹53.10/week`

### Payout Calculation

```
Payout = min(
    disrupted_hours × worker_avg_hourly_rate,
    plan_weekly_cap × (disrupted_hours / 8)
)

worker_avg_hourly_rate = trailing_28_day_earnings / total_active_hours
```

---

## ⚡ Parametric Triggers

All triggers are **automated, objective, and require zero worker input.**

### Trigger 1 — Heavy Rain (`TRIGGER_HEAVY_RAIN`)
| Parameter | Threshold |
|-----------|-----------|
| Rainfall intensity | > 15mm/hr sustained for > 30 min |
| Data source | OpenWeatherMap API + IMD alerts |
| Zone validation | Worker GPS must be in registered zone |
| Payout condition | Platform order volume drops > 40% in zone |
| Coverage window | Duration of alert + 30 min buffer |

### Trigger 2 — Extreme Heat (`TRIGGER_EXTREME_HEAT`)
| Parameter | Threshold |
|-----------|-----------|
| Temperature | > 42°C between 11am – 3pm |
| Data source | IMD Weather API |
| Zone validation | Worker's city must match alert region |
| Payout condition | Midday shift hours lost (capped at 3 hrs/day) |
| Coverage window | 11am – 3pm during alert |

### Trigger 3 — Severe Air Quality (`TRIGGER_AQI_HAZARD`)
| Parameter | Threshold |
|-----------|-----------|
| AQI level | > 300 (Severe category) for > 2 hrs |
| Data source | CPCB AQI API / OpenAQ |
| Zone validation | City-level match |
| Payout condition | Platform volume drop > 35% confirmed |
| Coverage window | Duration of Severe AQI period |

### Trigger 4 — Zone Curfew / Strike (`TRIGGER_CIVIL_DISRUPTION`)
| Parameter | Threshold |
|-----------|-----------|
| Source | Government alert API + verified news API |
| Zone validation | Worker GPS confirms inability to enter zone |
| Payout condition | Worker was scheduled (had recent activity in past 48 hrs) |
| Coverage window | Declared disruption period |

### Trigger 5 — Platform Outage (`TRIGGER_PLATFORM_OUTAGE`)
| Parameter | Threshold |
|-----------|-----------|
| Condition | Delivery platform API returns errors for > 45 min |
| Data source | Platform status API + synthetic uptime monitor |
| Zone validation | Worker was online (app active) during outage |
| Payout condition | Zero orders assigned despite worker being online |
| Coverage window | Verified outage duration |

> **Note:** All triggers require corroboration from at least 2 independent data signals before payout is initiated. Single-signal triggers are blocked and flagged for review.

---

## 🤖 AI/ML Integration

### 1. Zone Risk Scoring Model (Premium Calculation)
- **Algorithm:** Gradient Boosting (XGBoost)
- **Features:** Historical weather events, strike frequency, zone elevation, seasonal patterns, city-level infrastructure index
- **Output:** Weekly zone risk multiplier (updated every Sunday for next week)
- **Training data:** 3 years of IMD weather records + news archive + municipal data (mock dataset for hackathon)

### 2. Worker Risk Profile Model
- **Algorithm:** Logistic Regression
- **Features:** Account age, claim history, GPS consistency score, platform tenure, delivery volume variance
- **Output:** Worker trust score (0–1), used in fraud gating
- **Updated:** After every claim event

### 3. Disruption Impact Predictor
- **Algorithm:** Time-series forecasting (Prophet / LSTM)
- **Features:** Historical order volume drops during past disruptions, zone density, time of day
- **Output:** Predicted income loss (validates payout amount)
- **Use:** Secondary check on payout quantum

### 4. Anomaly Detection (Fraud Layer)
- **Algorithm:** Isolation Forest + rule-based thresholds
- **Features:** GPS trajectory, cell tower vs. GPS consistency, claim frequency, cross-worker claim clustering
- **Output:** Fraud probability score (0–1); auto-block if > 0.75

---

## 🔐 Fraud Detection Architecture

GigShield's fraud system uses a **3-signal validation gate.** All three signals must align for a payout to proceed automatically. A mismatch routes the claim to a soft-hold queue for insurer review.

```
Signal 1 — External Event Verified
    ↓ (AND)
Signal 2 — Worker Location Confirmed in Affected Zone
    ↓ (AND)  
Signal 3 — Platform Activity Confirms Income Loss
    ↓
Auto-Approve Payout

Any signal mismatch → Fraud Guard Review Queue
```

### Specific Fraud Vectors Addressed

| Fraud Type | Detection Method |
|------------|-----------------|
| GPS spoofing | Cell tower triangulation vs. reported GPS coordinates |
| Fake weather claims | Weather API independently verified; not worker-reported |
| Duplicate claims | Policy ID + event ID deduplication across all workers in same zone |
| Claim clustering | >3 workers claiming same event in same zone triggers secondary review |
| Inactive workers claiming | Must show platform "online" status in past 2 hours before event |
| Premium without intent to work | Workers with <5 orders in past 7 days excluded from auto-payout (manual review) |

---

## 📱 Platform Choice & Justification

**Chosen Platform: Progressive Web App (PWA) + WhatsApp Bot**

| Factor | Reasoning |
|--------|-----------|
| **PWA over native app** | No App Store friction; works on low-end Android devices; installable; offline-capable for dashboard viewing |
| **WhatsApp integration** | 500M+ Indian users; zero learning curve; workers already use it daily; enables payout notifications and weekly plan activation via chat |
| **Web admin dashboard** | Insurer/admin operations require full-screen analytics — browser is the right surface |
| **No iOS native app** | Q-Commerce partners in India are 95%+ Android users; native iOS adds cost without reach |

---

## 🛠️ Tech Stack

React, Vite, Tailwind CSS, Recharts, Leaflet, Node.js, Express, PostgreSQL, Redis, Python, FastAPI, XGBoost, Scikit-learn, OpenWeatherMap, CPCB AQI, Razorpay, Twilio, Vercel, Render, GitHub Actions

---

## 📅 Development Plan

### Phase 1 — Ideation & Foundation (Weeks 1–2, due March 20)
- [x] Problem research and persona definition
- [x] Application workflow design
- [x] Weekly premium model design
- [x] Parametric trigger specification
- [x] AI/ML integration plan
- [x] Tech stack selection
- [ ] Basic project scaffolding (React app + Node.js API skeleton)
- [ ] Zone risk mock dataset creation
- [ ] 2-minute pitch video

### Phase 2 — Automation & Protection (Weeks 3–4, due April 4)
- [ ] Worker onboarding flow (OTP, platform linking, zone selection)
- [ ] Insurance policy creation + weekly renewal logic
- [ ] Dynamic premium calculation (ML zone risk model integrated)
- [ ] 5 automated trigger implementations (weather + curfew + platform APIs)
- [ ] Zero-touch claim initiation pipeline
- [ ] WhatsApp notification on payout
- [ ] Basic claims management UI
- [ ] 2-minute demo video

### Phase 3 — Scale & Optimise (Weeks 5–6, due April 17)
- [ ] Fraud detection system (3-signal gate + Isolation Forest model)
- [ ] GPS spoofing detection
- [ ] Razorpay sandbox payout integration
- [ ] Worker dashboard: coverage status, payout history, weekly plan
- [ ] Insurer admin dashboard: loss ratios, disruption heatmap, fraud queue
- [ ] Predictive analytics: next-week disruption forecast for admin
- [ ] Final 5-minute demo video
- [ ] Final pitch deck (PDF)

---

## 👥 Team

| Name | Role |
|------|------|
| Jai Akash V | Full-stack development |
| T V Varun | ML/AI engineering |
| Kumaaragurubaran M | Backend + API integrations |
| Vaibhav Rajgupta | UI/UX + frontend |
| Srimantika Gangopadhyay | Research & Documentation |

**Institution:** SRM Institute of Science and Technology, Kattankulathur  
**GitHub Repository:** _(This repo)_  
**Demo Video (Phase 1):** _(Link to be added)_

---

## 📋 Critical Constraints Compliance

| Constraint | GigShield Approach |
|------------|-------------------|
| ❌ No health/life/accident/vehicle coverage | Strictly income-loss only; all triggers are external environmental/social events |
| ✅ Weekly pricing model | All plans priced and activated weekly; dynamic ML adjustment runs every Sunday |
| ✅ Parametric automation | 5 automated triggers; zero manual claim filing by worker |
| ✅ Fraud detection | 3-signal validation gate + Isolation Forest anomaly model |
| ✅ AI/ML integration | Zone risk scoring, worker trust scoring, disruption impact prediction |

---

> *GigShield is built for the Guidewire DEVTrails 2026 University Hackathon. All external API integrations use free tiers or sandbox/mock modes.*
