# SCM Assistant Bot
Supply Chain Management Chatbot built with Flowise RAG

## Public Chatbot URL
https://cloud.flowiseai.com/chatbot/2718a846-1763-491d-b669-d6a2232d2082

## Models Used
- **LLM:** Google Gemini (gemini-3.1-flash-lite-preview), Temperature: 0
- **Embeddings:** MistralAI (mistral-embed), Batch Size: 50
- **Vector Store:** Pinecone (index: scm-bot, similarity search)
- **Memory:** Buffer Window Memory (k=4)

## Chunk Configurations Tested

| Config | Splitter | Chunk Size | Overlap | PDF Chunks | CSV Chunks |
|--------|----------|------------|---------|------------|------------|
| A | Character Text Splitter | 1000 | 200 | 8 | 2,000 |
| B (Active) | Recursive Character Text Splitter | 500 | 100 | 35 | 4,000 |

Config B is significantly better — PDF improved from 8 to 35 chunks,
making individual policy sections retrievable.

## Sample Q&A Answers

**Q1: Which Tier-3 suppliers have an active disruption flag, and what response level applies per policy?**

11 Tier-3 suppliers: Dravex Components India, Plataforma Metales SA, Maghreb Castworks, Helios Pack Greece, Cerromax Mineria, Orinoco Pack SAPI, Quetzal Textiles, Sibertek Molding, Archipelago PCB Corp, Varna Electronics EAD, Deltaforge Vietnam. All are High Risk with an active flag → Level 3 Activate per Policy §9 (CPO escalation + alternate supplier at minimum 40% volume).

**Q2: Which suppliers qualify for the annual Volume Rebate Program and how many are there?**

19 suppliers qualify: Borealis Composites, Crestline Chemical Supply, Fenwick Alloy Solutions, Hanguk Circuit Works, Hokkaido Alloy Tech, Krauss-Polymex GmbH, Lakeshore Components, Lumivex Semiconductor NL, Maplewood Polymer Corp, Norbec Alloy Works, Nordloom Finland Oy, Orrentek Precision Mfg, Ostwind Composites AG, PrecisionForge Taiyuan, Solveig Eco Packaging, Straits Packaging Hub, Tasman Circuit Boards, Toreval Electronics, Valdoro Special Alloys. Criteria (Policy §4.2): Tier-1 + OTD ≥ 93% + Defect < 0.5% + Sustainability Score ≥ 85.

**Q3: Which region has the highest total PO value, and does it breach the concentration limit?**

EMEA at $193,987,179.91 — approximately 48.5% of total spend ($399,563,494.10). This breaches the 45% regional concentration cap (Policy §5.3), requiring a Diversification Plan within 60 days.

**Q4: Which suppliers are on Supplier Watch List (SWL) status and what does it restrict?**

11 suppliers (Compliance Score < 60): Deltaforge Vietnam, Maghreb Castworks, Helios Pack Greece, Cerromax Mineria, Orinoco Pack SAPI, Varna Electronics EAD, Quetzal Textiles, Plataforma Metales SA, Archipelago PCB Corp, Dravex Components India, Sibertek Molding. SWL restricts new PO issuance to 20% of prior quarter volume (Policy §3.4).

**Q5: Which product category has the highest average defect rate and does it exceed the Tier-2 limit?**

Mechanical Components — average 2.12% across 360 POs. Below the Tier-2 ceiling of 2.50% (Policy §3.2), so no breach — but approaching the limit.

## What I'd Improve
- Add metadata filtering (supplier_id, region, tier) for precise pre-filtering
- Replace CSV RAG with a SQL agent for exact aggregation queries
- Add a cross-encoder re-ranker for better retrieval quality
- Build automated eval pipeline using RAGAS metrics
- Add LangSmith observability for production monitoring
