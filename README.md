# AgriAgent 🌾
### Autonomous AI Agents for Smarter Agriculture

> *Empowering farmers with intelligent, decentralized agents that negotiate prices, predict crop risks, unlock credit, and trace supply chains — in real time.*

---

## 📌 Overview & Project Summary

AgriAgent is a multi-agent AI system built on **ASI-1** that serves as an intelligent economic backbone for smallholder farmers in India and emerging markets. By deploying a network of autonomous agents — each specialized in a distinct domain (market negotiation, weather intelligence, credit access, and supply chain traceability) — AgriAgent eliminates the information asymmetry that costs Indian farmers an estimated **₹1.5 lakh crore annually**.

| Attribute | Details |
|---|---|
| **Project Name** | AgriAgent |
| **Theme** | Social Good / Education |
| **Target Users** | Smallholder farmers, agricultural cooperatives, rural lenders |
| **Primary Region** | India (scalable globally) |
| **Core Technology** | ASI-1 (Fetch.ai), Python, React, SMS Gateway |
| **Team Size** | Solo |

---

## 🔴 Problem Statement

### The Reality of Indian Agriculture

India has **~140 million smallholder farmers** who collectively produce over 50% of the nation's food supply. Yet the majority live below or near the poverty line. The root causes are systemic and well-documented:

**1. Price Exploitation**
Farmers sell at farm-gate prices set by middlemen (mandis/arthiyas) with zero negotiating power. A farmer selling tomatoes for ₹2/kg watches the same tomatoes sell for ₹40/kg in a city market 3 hours away. The farmer captures less than 5% of final retail value.

**2. Weather & Crop Loss**
Over **50% of crop losses** in India are attributable to weather events that were predictable 3–7 days in advance. Farmers lack access to hyperlocal, actionable intelligence — generic weather apps don't tell you *"delay your harvest by 2 days to avoid the approaching rainfall"*.

**3. Credit Desert**
Despite government schemes, **76% of rural farmers** still rely on informal moneylenders charging 36–60% annual interest. Formal banks require collateral that smallholders don't have, and loan processing takes weeks — far too slow for planting season decisions.

**4. Supply Chain Opacity**
From farm to fork, a commodity passes through 6–8 intermediary hands. There is no traceability. Consumers can't verify origin. Farmers can't prove quality. Food safety incidents are impossible to trace efficiently.

### Current Solutions & Their Limitations

| Existing Solution | Limitation |
|---|---|
| eNAM (National Agriculture Market) | Adoption is low; interface is complex; no real-time negotiation |
| Kisan Suvidha App | Information-only; no action layer; no agents |
| Commodity SMS Alerts | Generic price data; no personalization or negotiation |
| Crop Insurance Schemes | Claim processes are slow; doesn't prevent loss |

**The gap:** No existing solution combines real-time intelligence, autonomous action, and decentralized trust in a single platform accessible to farmers with basic smartphones.

---

## 💡 Solution Overview & Unique Value Proposition

AgriAgent deploys **four specialized ASI-1 agents** that work in concert as a farmer's invisible economic team:

```
┌─────────────────────────────────────────────────────────┐
│                   FARMER INTERFACE                       │
│              (SMS / WhatsApp / Mobile App)               │
└─────────────────────┬───────────────────────────────────┘
                      │
         ┌────────────▼────────────┐
         │    AgriAgent Orchestrator (ASI-1)    │
         │    Routes queries to specialized agents  
         └──┬──────┬────────┬────────┬──────────┘
            │      │        │        │
     ┌──────▼─┐ ┌──▼───┐ ┌─▼────┐ ┌─▼──────┐
     │ Price  │ │Weather│ │Credit│ │Supply  │
     │Negotiate│ │ Intel │ │ Agent│ │Chain   │
     │ Agent  │ │ Agent │ │      │ │ Agent  │
     └────────┘ └───────┘ └──────┘ └────────┘
```

### The Four Agents

**🤝 PriceAgent** — Autonomously monitors real-time mandi prices across 50+ markets, identifies the best buyer for a farmer's produce, and initiates negotiation on their behalf. Farmers receive a verified offer without stepping foot in a mandi.

**🌦️ WeatherAgent** — Ingests hyperlocal satellite and ground sensor data, models crop-specific risk (pest likelihood, irrigation needs, harvest windows), and pushes proactive alerts 48–72 hours before actionable decisions are needed.

**💰 CreditAgent** — Evaluates a farmer's soil health reports, crop history, and weather risk profile to generate a real-time creditworthiness score. Automatically submits micro-loan applications to partnered rural lenders with pre-filled documentation.

**🔗 TraceAgent** — Records each supply chain handoff on a shared ledger. Generates QR-code provenance certificates that buyers, retailers, and consumers can verify. Builds reputation scores for farmers over time.

### Unique Value Proposition

> AgriAgent is the only system where autonomous agents *act* on behalf of farmers — not just inform them. The farmer doesn't need to learn a new platform; the agents come to them via SMS.

---

## 🤖 ASI-1 Integration

### Why ASI-1 is the Right Foundation

ASI-1 (Fetch.ai's autonomous agent framework) is architecturally perfect for AgriAgent because:

- **Agent autonomy** — ASI-1 agents can initiate actions, negotiate with other agents, and complete transactions without human intervention at each step
- **Decentralized trust** — No central authority controls the marketplace; agents interact peer-to-peer via the Fetch.ai network
- **Interoperability** — ASI-1 agents can connect to external APIs (weather, banking, logistics) natively
- **Scalability** — New specialized agents can be added to the network without rebuilding the core

### Agent Architecture & API Endpoints

```python
# ASI-1 Agent Definition Example — PriceAgent
from uagents import Agent, Context, Model

class PriceQuery(Model):
    farmer_id: str
    crop_type: str
    quantity_kg: float
    location: str

class PriceOffer(Model):
    buyer_id: str
    price_per_kg: float
    pickup_date: str
    confidence_score: float

price_agent = Agent(
    name="price_negotiator",
    seed="agriagent_price_seed",
    endpoint=["http://localhost:8000/submit"]
)

@price_agent.on_message(model=PriceQuery)
async def handle_price_query(ctx: Context, sender: str, msg: PriceQuery):
    # Query live mandi prices via external API
    market_data = await fetch_mandi_prices(msg.crop_type, msg.location)
    best_offer = negotiate_best_price(market_data, msg.quantity_kg)
    await ctx.send(sender, PriceOffer(**best_offer))
```

### Data Flow

```
Farmer SMS "sell 500kg tomato Nashik"
        ↓
SMS Gateway → AgriAgent API
        ↓
Orchestrator Agent (ASI-1) parses intent
        ↓
PriceAgent queries 50+ mandis via eNAM API
        ↓
PriceAgent negotiates with registered BuyerAgents
        ↓
Best offer returned → SMS confirmation to farmer
        ↓
TraceAgent logs transaction on ledger
```

### ASI-1 Interaction Log (Documented)

During ideation, ASI-1 was used to:
1. **Validate agent roles** — *"Given a smallholder farmer in Maharashtra with 500kg of onions, what autonomous agent actions would deliver the highest economic value?"* → Output shaped the four-agent architecture
2. **Refine negotiation logic** — *"Design a negotiation protocol between a FarmerAgent and BuyerAgent that prevents price manipulation"* → Output informed the auction mechanism
3. **Stress-test edge cases** — *"What happens if WeatherAgent and CreditAgent give conflicting recommendations about planting a new crop?"* → Output defined the conflict resolution hierarchy
4. **Generate SMS templates** — ASI-1 generated farmer-facing message templates in Hindi and regional languages

---

## 🗺️ Implementation Roadmap

### Phase 1 — Foundation (Weeks 1–3)
- [ ] ASI-1 agent scaffolding (4 base agents)
- [ ] eNAM API integration for price data
- [ ] SMS gateway setup (Twilio/MSG91)
- [ ] Farmer registration flow

### Phase 2 — Intelligence Layer (Weeks 4–6)
- [ ] WeatherAgent — IMD API + satellite data integration
- [ ] PriceAgent — negotiation protocol with BuyerAgents
- [ ] Basic mobile web dashboard

### Phase 3 — Credit & Trust (Weeks 7–9)
- [ ] CreditAgent — soil health + crop history scoring model
- [ ] Partner lender API integrations (NABARD ecosystem)
- [ ] TraceAgent — supply chain ledger (Fetch.ai CosmWasm)

### Phase 4 — Pilot (Weeks 10–12)
- [ ] Pilot with 50 farmers in 2 districts (Nashik, Pune)
- [ ] Feedback loops and agent retraining
- [ ] Hindi + Marathi language support

### Phase 5 — Scale (Month 4+)
- [ ] Expand to 5 states
- [ ] Onboard 500+ registered buyers
- [ ] Government partnership for PMFBY insurance integration

---

## 🏗️ Technical Architecture & Technology Stack

```
┌─────────────────────────────────────────────────────────────┐
│                     FRONTEND LAYER                          │
│         React PWA + SMS Interface (Twilio)                  │
└─────────────────────────┬───────────────────────────────────┘
                          │ REST / WebSocket
┌─────────────────────────▼───────────────────────────────────┐
│                    BACKEND LAYER                            │
│              Python FastAPI + Agent Orchestrator            │
└──────┬──────────────────┬──────────────────┬───────────────┘
       │                  │                  │
┌──────▼──────┐  ┌────────▼──────┐  ┌───────▼────────┐
│  ASI-1      │  │  PostgreSQL   │  │  Redis Cache   │
│  Agent Network│  │  Farmer DB    │  │  Price Cache   │
└─────────────┘  └───────────────┘  └────────────────┘
       │
┌──────▼──────────────────────────────────────────────┐
│              EXTERNAL INTEGRATIONS                   │
│  eNAM API · IMD Weather · NABARD · Satellite APIs   │
└─────────────────────────────────────────────────────┘
```

| Layer | Technology |
|---|---|
| Agent Framework | ASI-1 (Fetch.ai uAgents) |
| Backend | Python 3.11, FastAPI |
| Frontend | React, Tailwind CSS |
| Database | PostgreSQL, Redis |
| Messaging | Twilio SMS, WhatsApp Business API |
| Supply Chain Ledger | Fetch.ai CosmWasm |
| Weather Data | IMD API, NASA POWER |
| Deployment | Docker, AWS EC2 |

---

## ⚡ Key Features

| Feature | Description | ASI-1 Role |
|---|---|---|
| **Smart Price Negotiation** | Agents scan 50+ mandis and negotiate on farmer's behalf | PriceAgent autonomously queries and negotiates with BuyerAgents |
| **Crop Risk Alerts** | 48–72hr proactive SMS warnings for weather events | WeatherAgent processes satellite data and triggers alerts autonomously |
| **Instant Micro-Credit** | Real-time creditworthiness score + auto loan application | CreditAgent scores farmer and submits to lender APIs without human intervention |
| **Supply Chain QR** | Scannable provenance certificate for every harvest batch | TraceAgent logs each handoff; generates verifiable QR certificates |
| **Multilingual SMS** | Communicates in Hindi, Marathi, Tamil — no app required | Orchestrator Agent handles language detection and routing |
| **Farmer Reputation** | Builds credit and quality history over time | Agents accumulate verified transaction history on the Fetch.ai network |

---

## 👥 Target Users & Market Size

**Primary Users**
- Smallholder farmers (< 2 hectares) — 120M in India
- Agricultural cooperatives — 800,000+ registered in India
- Rural microfinance institutions — 20,000+ active lenders

**Secondary Users**
- Food aggregators and exporters seeking traceable supply
- Insurance companies needing crop risk data
- Government agencies monitoring agricultural economics

**Market Size**
- Indian agricultural market: **$400B+**
- AgriTech investment in India (2025): **$1.2B**
- Target addressable market (digital farm services): **$24B by 2027**

---

## 🌍 Impact & Benefits

### Social Impact
- Farmers capture **30–50% more value** from their produce through direct negotiation
- Reduction in farmer debt cycles through accessible formal credit
- Weather intelligence prevents estimated **20–30% of avoidable crop losses**
- Digital identity and reputation built for previously undocumented farmers

### Economic Impact
- Reduces middlemen extraction estimated at **₹1.5 lakh crore/year**
- Increases formal credit penetration in rural India
- Enables premium pricing for traceable, quality-verified produce

### Environmental Impact
- Optimized harvest timing reduces food waste at farm level
- Supply chain traceability enables carbon footprint tracking per commodity
- Precision irrigation recommendations from WeatherAgent reduce water usage

---

## ⚠️ Challenges & Mitigation

| Challenge | Risk Level | Mitigation Strategy | ASI-1's Role |
|---|---|---|---|
| Low smartphone penetration | High | SMS-first interface, no app required | Agents communicate via SMS gateway |
| Farmer trust in AI | High | Transparent agent actions; human override always available | Agents explain every recommendation in plain language |
| Data quality (mandi prices) | Medium | Cross-validate across 3+ sources; flag anomalies | PriceAgent detects price manipulation via statistical outlier detection |
| Internet connectivity in rural areas | High | Offline-capable PWA; SMS fallback | Agents cache last known data and operate on delayed sync |
| Regulatory compliance (lending) | Medium | Partner with NABARD-registered institutions only | CreditAgent only connects to approved lender endpoints |
| Agent coordination conflicts | Low | Defined priority hierarchy; Orchestrator arbitrates | ASI-1 Orchestrator has conflict resolution protocol |

---

## 🔮 Future Scope

- **Satellite field monitoring** — Computer vision agents that analyze drone/satellite imagery to detect crop disease before visible symptoms appear
- **Cross-border expansion** — Deploy in Bangladesh, Nigeria, Kenya where identical problems exist
- **Carbon credit marketplace** — Agents that automatically calculate and sell carbon credits for regenerative farming practices
- **Cooperative formation** — Agents that identify and form virtual cooperatives among farmers with complementary crops for bulk negotiation leverage
- **ASI-1 Marketplace** — List specialized AgriAgents on the Fetch.ai agent marketplace for third-party developers to build on

---

## 👤 Team Information

| Field | Details |
|---|---|
| **Name** | Abdoulaye Sy Ndaw |
| **Role** | Full-Stack Developer & AI Engineer |
| **Institution** | École Polytechnique de Thiès (EPT), Senegal |
| **Background** | Built EduBox — offline AI tutoring platform on Raspberry Pi (RAG + ChromaDB + LLM) |
| **Skills** | Python, Java, React, RAG pipelines, AI agent systems |

---

## 📚 References & Resources

- [Fetch.ai uAgents Documentation](https://docs.fetch.ai/uAgents/)
- [ASI-1 Model Overview](https://fetch.ai/asi-1)
- [eNAM API — National Agriculture Market](https://www.enam.gov.in)
- [IMD Weather API — India Meteorological Department](https://mausam.imd.gov.in)
- [NABARD Rural Credit Framework](https://www.nabard.org)
- [World Bank — Agriculture in India Report 2024](https://www.worldbank.org/en/country/india/publication/agriculture)
- [Fetch.ai CosmWasm Smart Contracts](https://docs.fetch.ai/CosmWasm/)

---

## ✅ Submission Checklist

- [x] Problem statement clearly defined
- [x] Solution approach with ASI-1 integration plan
- [x] ASI-1 interactions documented
- [x] Implementation roadmap with milestones
- [x] Technical architecture defined
- [x] Target users and market size quantified
- [x] Impact metrics specified
- [x] Challenges and mitigations addressed
- [x] GitHub repository structure ready

---

*Built with ASI-1 for Ideathon 2026 — Tech Z*
