# Proposal: 1000 ICP-Qualified Companies in One Month
## DeepThought Business Analytics Internship — Part B
### Sourcing Strategy + Scale-Up Plan

---

## Goal

Build a verified list of 1,000 companies matching DeepThought's Federer ICP — Indian specialty manufacturers, Rs.50Cr–Rs.500Cr revenue, promoter-driven, differentiated product, technical decision-maker, active growth signals — within 30 calendar days.

---

## Key Constraints

- **Quality over volume.** 1,000 genuinely ICP-qualified companies, not 5,000 names from a bulk dump. Every company must have evidence-backed scores on all 6 criteria.
- **Yield reality**: From Part A research, roughly 1 in 10 companies investigated will pass (10-15% yield) when targeting unlisted private MSMEs in chemical/biotech clusters. To get 1,000 passes, the sourcing universe needs to be ~8,000–10,000 companies.
- **The unlisted MSME problem**: The most ICP-relevant companies have no digital presence. Standard web-scraping/AI scoring pipelines work well for listed companies but miss the core ICP. The proposal must account for this.
- **Tools available**: Claude, Gemini, GitHub Copilot, Antigravity, scraping tools, database subscriptions, API credits.

---

## The Funnel

```
Raw universe (8,000–10,000 companies)
    ↓ Hard pre-filters (auto-disqualify)
Filtered pool (5,000–6,000)
    ↓ AI-assisted ICP scoring (6 criteria)
First-pass qualified (1,200–1,500)
    ↓ Human QA on borderline + low-confidence
Final verified list (1,000)
```

---

## Sourcing Strategy (Part B, Question 1)

### Why Standard Google Search Is Insufficient

Google search surfaces companies that have digital presence. The most ICP-aligned companies — privately-held specialty chemical or biotech MSMEs with Rs.50-300 Cr revenue — often have: no website, no LinkedIn, no press coverage. They operate in MIDC clusters, CETP zones, and industrial estates. They are known to their customers and suppliers, not to search engines. We need sources that find companies regardless of digital footprint.

---

### Source 1: DSIR Recognized R&D Units List

**What**: Department of Scientific and Industrial Research maintains a directory of companies with recognized in-house R&D units. 2024 edition lists 1,957 companies with 2,501 R&D units.

**Why it works for this ICP**:
- DSIR recognition directly signals C3 (differentiation — company invested in R&D formally) and C4 (technical decision-maker — someone scientific leads the R&D unit).
- It's a government-issued pre-filter for technical seriousness. Commodity traders and services companies don't have DSIR-recognized R&D.
- The 2024 list is downloadable from dsir.gov.in as PDF.

**How to extract**: Parse the PDF with Python (pdfplumber or Camelot), extract company names, addresses, and industry types. Filter to manufacturing companies in target segments and target cities.

**Expected yield after filtering to target segments and cities**: 800–1,000 companies.

**Limitations**: Skews toward older, established companies. Misses younger companies (< 5 years) that haven't applied for DSIR recognition yet. Also requires manual cross-referencing with websites — DSIR list only gives registered addresses, not websites.

---

### Source 2: CETP (Common Effluent Treatment Plant) Member Directories

**What**: Every chemical or pharmaceutical industrial zone with MIDC designation in India has a CETP (Common Effluent Treatment Plant) that serves member manufacturers. CETP operators maintain membership lists. Unlike MIDC lists (which include all industries), CETP members are specifically chemical/pharma manufacturers because CETP membership is mandatory for manufacturers producing regulated effluent.

**Why it works for this ICP**:
- CETP membership = confirmed chemical/pharma manufacturer. Eliminates traders, service companies, and assembly shops in one step.
- Target CEPTs: Kurkumbh CETP (Pune), Patancheru CETP (Hyderabad), GIDC Ankleshwar CETP (Gujarat), Tarapur CETP (Maharashtra), Nanjangud CETP (Karnataka).
- In the Part A research, Kurkumbh CETP was referenced directly — it covers Pune's main chemical zone.

**How to extract**: CETP member lists are sometimes available on MPCB (Maharashtra Pollution Control Board) portals or directly from CETP management. Some CETP members are listed in public environmental reports. File RTI with MPCB for member lists of major CEPTs.

**Expected yield**: 400–600 companies per major CETP zone. Across 8–10 target CETP zones: 2,000–3,000 unique companies.

**Limitations**: Accessing full CETP membership lists may require RTI (Right to Information) requests, which take 30 days. Some CEPTs may not maintain digital directories. This source works best for Phase 2 (second month onward) or if Antigravity can pull MPCB portal data directly.

---

### Source 3: USFDA/EU-GMP/WHO-GMP Approved Facility Lists

**What**: USFDA publishes a public database of approved drug manufacturing facilities (fda.gov). EU-GMP database is at eudralex.eu. WHO prequalification list is at who.int. All are freely accessible.

**Why it works for this ICP**:
- Regulatory approval = confirmed manufacturer (C1), differentiation (C3 — regulatory compliance is a high barrier), and export market access (C5 tailwind).
- USFDA-approved Indian facility = company exports to the US, which means revenue and growth evidence.
- Filtering to MSME-sized Indian facilities (exclude Cipla, Sun, Dr. Reddy's) gives a targeted list.

**How to extract**: USFDA facility database is searchable by country. Filter: country = India. Extract facility name, address, and approval type. Cross-reference address to target city clusters. For non-pharma segments (specialty chemicals for electronics, agrochem), check REACH (European Chemicals Agency) registrations by Indian exporters.

**Expected yield**: 300–500 companies after filtering to MSME scale and target segments.

**Limitations**: Heavy bias toward pharma and bulk API. Electronics chemicals, agrochem intermediates, and performance chemicals are less represented. For non-pharma specialty chemicals, switch to REACH database or export promotion council members.

---

### Source 4: BSE SME / NSE Emerge + Tofler MCA Data

**What**: BSE SME Platform and NSE Emerge list small-cap companies. Tofler and Zauba Corp provide MCA (Ministry of Corporate Affairs) data including paid-up capital, NIC code, and director details.

**Why it works for this ICP**:
- BSE SME: 500+ manufacturing companies listed with publicly available financials (revenue, promoter holding, sector). Enables immediate revenue band and promoter holding scoring.
- MCA/Tofler: Filters by NIC code (manufacturing sector codes) + city + paid-up capital range. Gives unlisted companies' approximate size proxy and director names.
- NIC codes for target segments: 2011 (basic chemicals), 2013 (specialty chemicals), 2100 (pharma), 2019 (agrochem), 2029 (other chemical products).

**How to extract**: BSE SME: download sector-wise company master from BSE website. For MCA: use Antigravity or Zauba Corp to query by NIC code + city + paid-up capital >₹1 Cr (proxy for revenue >₹50 Cr companies).

**Expected yield**: 400–600 BSE SME companies in target segments. 1,000–2,000 from MCA NIC code queries (but very noisy — 60-70% will be non-manufacturing on verification).

**Limitations for MCA**: NIC codes are self-reported by companies and often incorrect. Paid-up capital is a poor revenue proxy. Many dormant companies in MCA database. Requires heavy filtering.

---

### Source 5: Export Promotion Council Member Directories

**What**: CHEMEXCIL (Basic Chemicals Exports Promotion Council), PHARMEXCIL (Pharmaceuticals Export Promotion Council), APCTT (Asia Pacific Centre for Technology Transfer), and FICCI/CII member directories.

**Why it works for this ICP**:
- Active export promotion council membership = company is exporting (C5 tailwind verified) and is a legitimate manufacturer (C1 — exporters must be producers or registered exporters).
- CHEMEXCIL members include specialty chemicals, performance chemicals, and fine chemicals exporters. PHARMEXCIL includes pharma intermediates and API exporters.
- These councils publish member directories (some publicly, some restricted).

**How to extract**: CHEMEXCIL and PHARMEXCIL directories are available online for registered users. Some are downloadable PDFs. Scrape member name + city + product category.

**Expected yield**: 500–800 companies across CHEMEXCIL and PHARMEXCIL, filtered to target cities and segments.

**Limitations**: Biased toward export-oriented companies. Does not capture companies that primarily serve domestic markets (some ICP fits may be domestic-focused).

---

### Source 6: Trade Expo Exhibitor Directories

**What**: Industry-specific expos publish exhibitor directories. Target expos for specialty chemicals/biotech: CPHI India (pharma/chem, annual), BioAsia (Hyderabad, biotech), ChemExpo India (annual, Mumbai), India International Pharma Expo (IIPE), ACREX (HVAC/industrial), AgroWorld.

**Why it works for this ICP**:
- Paying Rs.2–10L for an exhibition booth signals C6 (growth intent — they are investing in business development).
- Expo segment tags map directly to our industry baskets.
- Exhibitor directories are public and include company name, website, city, and product category.

**How to extract**: Scrape exhibitor directories from expo websites. Use Playwright (JavaScript-heavy sites) or BeautifulSoup (HTML). For past expos, check Wayback Machine or cached versions.

**Expected yield**: 500–700 companies across 5–6 expos after deduplication.

**Limitations**: Biased toward companies that can afford booths — misses bootstrapped Rs.50-100 Cr companies. Some smaller MSMEs only attend, not exhibit.

---

### Source 7: LinkedIn Sales Navigator (Inverted Search)

**What**: Instead of finding companies first and then checking if the DM is technical, find technical DMs first and check if their company is a specialty manufacturer.

**Why it works for this ICP**:
- Filters: Industry (pharma, chemicals, biotech), Company size (50–500 employees), Geography (target cities), Seniority (Founder, Owner, MD, Director), Function (Engineering, R&D, Manufacturing, Operations).
- Finds engineer/scientist founders at manufacturing companies — exactly the C4 criterion.
- Also useful for finding Gen-2 technical leaders (MBA from IIM + B.Tech from IIT/NIT — the profile the assignment highlights).

**How to extract**: Sales Navigator allows CSV export of up to 2,500 profiles per search. Run multiple targeted searches by city and sector. Extract to CSV.

**Expected yield**: 400–600 unique companies across target cities.

**Limitations**: LinkedIn headcount and industry classification are self-reported and often wrong for Indian MSMEs. Many founder-promoters of Rs.50-100 Cr companies don't have LinkedIn profiles.

---

### Source 8: Government Scheme Beneficiary Lists (Creative/Unconventional)

**What**: Several government schemes publish beneficiary lists: (a) DSIR's Technology Development and Demonstration Programme (TDDP) grant recipients; (b) National Science and Technology Entrepreneurship Development Board (NSTEDB) supported companies; (c) SIDBI's "SMILE" loan scheme for MSME manufacturers; (d) PLI scheme applicants for bulk drugs, medical devices, and specialty chemicals (Ministry of Chemicals and Fertilizers).

**Why it works for this ICP**:
- TDDP grant = confirmed manufacturer investing in R&D (C1 + C3)
- PLI applicant = confirmed manufacturer in growing sector with regulatory engagement (C1 + C3 + C5)
- SIDBI loan = confirmed Indian MSME manufacturer with formal banking relationship (C1 + revenue band proxy)

**How to extract**: PLI beneficiary lists are publicly available through Ministry of Chemicals website. DSIR TDDP grant lists are published annually. RTI request can obtain SIDBI SMILE loan beneficiary lists for specific NIC codes and cities.

**Expected yield**: 200–400 companies but very high precision — these companies have already passed government technical screening.

**Limitations**: PLI scheme is primarily bulk drugs and APIs — limited coverage of performance chemicals. RTI has a 30-day response window. Annual TDDP lists may not be current.

---

## The 1,000-Company Proposal (Part B, Question 2)

### Week 1: Build the Raw Universe

**Goal**: Assemble 8,000–10,000 candidate companies with minimum fields: name, city, segment tag, website or MCA address.

| Day | Task |
|-----|------|
| 1–2 | Download and parse DSIR 2024 list, BSE SME company master (chemicals/pharma/biotech sectors), PHARMEXCIL and CHEMEXCIL directories. Structured data — fastest to process. Estimated: 2,500 companies. |
| 2–3 | Scrape CPHI India 2024, ChemExpo India 2024, BioAsia 2025 exhibitor directories using Python/Playwright. Estimated: 600 companies. |
| 3–4 | Antigravity MCA query: NIC codes 2011, 2013, 2100, 2019, 2029 + target cities (Pune, Hyderabad, Ahmedabad, Chennai, Bengaluru, Vadodara, Coimbatore) + paid-up capital >₹1 Cr. Estimated: 3,000+ companies (noisy). |
| 4–5 | LinkedIn Sales Navigator: 5 searches × target cities × chemical/pharma segments. Export profiles. Estimated: 600 companies. |
| 5–6 | USFDA facility database: filter India + manufacturing + exclude big-pharma (Cipla, Sun, DRL, Lupin, Zydus, etc. by name). Estimated: 500 companies. |
| 6–7 | Deduplicate master list: fuzzy name matching (Python fuzzywuzzy/rapidfuzz) + CIN number matching for listed companies. Resolve "ABC Pvt Ltd" vs "ABC Private Limited" variants. |
| 7 | Website discovery for the ~40% without URLs: Google search automation via Claude API — "{company name} {city} specialty chemicals". Run 3,000 searches, extract first relevant URL per company. |

**Week 1 output**: 8,000–10,000 unique candidates. ~60% have website URLs.

---

### Week 2: Hard Pre-Filter + Automated ICP Scoring

**Goal**: Score all candidates on 6 criteria using AI. Reduce universe to ~1,200–1,500 first-pass passes.

#### Hard Pre-Filter (Before AI Scoring — Auto-Reject)

These checks run in seconds via regex/string matching on company name and available data:

1. Company name contains: "Trading", "Traders", "Import", "Export", "Agency", "Distributor", "Sales", "Marketing" → likely trader, not manufacturer
2. Company name contains: "Services", "Consultancy", "Advisory", "Solutions" without "Manufacturing" → likely services
3. Company name contains: "Lab", "Laboratories" without "Manufacturing" → verify CRO vs manufacturer
4. Revenue > Rs.500 Cr (where known from BSE data) → auto-reject for revenue ceiling
5. No website found after 2 Google search attempts → flag for human review (not auto-reject — many ICP companies have no website)
6. PE ownership signals in company description → flag for human review

**Expected to eliminate**: 2,000–3,000 companies before AI scoring.

#### AI Scoring Pipeline

For each remaining company (~6,000):

**Step 1: Scrape website** (where available)
- Pages: /, /about, /products, /team, /news, /careers, /contact
- Tool: Playwright (JavaScript-heavy) + requests (static). Max 8,000 tokens per company.
- Skip if no website → go to MCA-only scoring (lower confidence)

**Step 2: Build scoring prompt for Claude Haiku**

```
You are a business analyst. Score this company against DeepThought's 6 ICP criteria for Indian specialty manufacturers.

Company: {name}
Website text: {scraped_text}

Score each criterion:
C1 Manufacturer: Weak / Moderate / Strong + one line evidence
C2 India-based: Weak / Moderate / Strong + evidence
C3 Differentiated: Weak / Moderate / Strong + evidence
C4 Technical DM: Weak / Moderate / Strong + evidence (name + credentials if found)
C5 Growing sector: Weak / Moderate / Strong + evidence
C6 Growth signals: Weak / Moderate / Strong + evidence

Revenue band estimate: <30Cr / 30-100Cr / 100-300Cr / 300-500Cr / >500Cr / Unknown
Confidence: High / Medium / Low
Verdict: Strong Pass / Pass / Borderline / Fail
Fail reason (if Fail): [most disqualifying criterion]

Respond ONLY in JSON.
```

**Step 3: Handle borderline cases**
- If Haiku verdict = "Borderline": re-score with Claude Sonnet
- If any criterion has confidence = "Low": flag for human QA
- If Fail on C1 (not manufacturer) or C4 (PE/conglomerate): auto-disqualify with reason

**Cost estimate:**
- Haiku first pass: ~₹0.45/company × 6,000 = ₹2,700
- Sonnet re-score: ~₹3.50/company × 1,200 = ₹4,200
- Total AI cost: ~₹7,000

**Speed:**
- Scraping: ~30 sec/company × 6,000 = 50 hours. Run 6 parallel scrapers = ~8 hours.
- Haiku scoring: ~3 sec/company = ~5 hours.
- Total: ~13 hours of compute.

**Week 2 output**: ~1,200–1,500 first-pass qualifications.

---

### Week 3: Re-scoring, QA, and Human Verification

**Goal**: Verify AI scoring accuracy. Target: final list of 1,200 verified companies to give headroom.

#### Key AI Failure Modes (from Part A research)

| Failure Mode | Why It Happens | QA Fix |
|---|---|---|
| C3 inflation: ISO 9001 scored as "differentiation" | LLM reads any certification as differentiating | Flag all C3=Strong cases where only ISO 9001/14001 mentioned. Require patents/DSIR/USFDA/proprietary product name. |
| C4 false positive: "Engineer" inferred from job title only | LLM guesses "technical" from "Manufacturing Director" title | Require academic institution name (IIT/NIT/BITS/IISc/UDCT/ICT) or PhD/M.Tech credential to score C4=Strong |
| C6 false positive: Stale news scored as growth | Press page has articles from 2020 → LLM scores growth as moderate | Flag any C6 evidence older than 2023. Growth signal must be post-2022. |
| C1 false negative: CRO/services company has "manufacturing" language | Companies say "we manufacture solutions" when they mean services | Add string check: if website contains "contract research", "testing services", "analytical services", "CRO" → flag C1 for human review |
| Trader trap: Distributor claims to be manufacturer | "We manufacture and supply" used by trading companies | Check for physical address of manufacturing plant (not just registered office). Look for "plant", "reactor", "manufacturing facility" in website text. |
| PE/conglomerate false pass | Subsidiary websites look like independent promoter companies | Check for: "subsidiary of", "part of [Group]", "wholly owned by" → flag C4 for human review |

#### Auto-QA Rules (Programmatic)

```python
flags = []
if c3_score == "Strong" and "ISO 9001" in c3_evidence and "patent" not in c3_evidence and "DSIR" not in c3_evidence and "USFDA" not in c3_evidence:
    flags.append("C3_inflation_check")
if c4_score == "Strong" and not any(inst in c4_evidence for inst in ["IIT", "NIT", "BITS", "IISc", "ICT", "UDCT", "PhD", "M.Tech"]):
    flags.append("C4_credential_missing")
if c6_score != "Weak" and max_year_in_c6_evidence < 2023:
    flags.append("C6_stale_news")
if "contract research" in website_text.lower() or "CRO" in website_text:
    flags.append("C1_possible_services")
if any(w in website_text.lower() for w in ["subsidiary of", "wholly owned", "part of group"]):
    flags.append("C4_possible_conglomerate")
```

#### Human QA Process (Days 19–24)

- Review all ~400 flagged companies: 3–4 minutes each = ~25 hours
- For each: open website, check 2–3 specific claims, adjust scores
- Spot-check 50 random Strong Pass companies (should be clean, verifies model quality)

**Week 3 output**: ~1,200 verified companies.

---

### Week 4: Final Assembly + Enrichment

**Goal**: Final list of 1,000 verified companies. Top 200 with personalization hooks.

| Day | Task |
|-----|------|
| 25–26 | Final list assembly. Merge Strong Pass + QA-verified Pass. Sort by Federer score (strong > pass > borderline). Take top 1,000. |
| 26–27 | Personalization hooks for top 200: use Claude Sonnet to generate specific, true outreach hooks. Prompt: "Given this company profile, write one sentence that a reader of their website would find specific and surprising, that could open an outreach email." Manual review of 200 hooks. |
| 27–28 | Format final deliverable: master CSV, summary dashboard, city/segment breakdown. |
| 28–29 | Source attribution: which source contributed how many final companies. |
| 30 | Buffer. |

---

## Weekly Summary

| Week | Focus | Output |
|------|-------|--------|
| 1 | Sourcing | 8,000–10,000 candidate companies from 7+ sources |
| 2 | Scraping + AI scoring | 1,200–1,500 first-pass qualifications |
| 3 | Re-scoring + Human QA | 1,200 verified companies |
| 4 | Final assembly | 1,000 verified list + top 200 with personalization hooks |

---

## Risk Mitigation

| Risk | Probability | Mitigation |
|------|------------|-----------|
| Yield lower than projected | Medium | Expand to additional CETP lists, state industrial authority directories (TSIIC Hyderabad, MIDC Maharashtra full directory), physical MIDC visits for target clusters |
| Unlisted MSME data quality too low | High | Accept lower confidence for unlisted companies; tier the list: Tier 1 (listed, verified), Tier 2 (unlisted, AI-scored), Tier 3 (unlisted, manual-verified). Tier 1 goes straight to outreach; Tier 3 needs phone call first. |
| Scraper blocked | Low-Medium | Rotate user agents, add politeness delays (2–5 sec), use residential proxy for high-priority sites. Fall back to manual for top-50 blocked sites. |
| AI scoring accuracy < 80% | Low-Medium | Test on 15 calibration companies before full run. Adjust prompt if <12/15 correct. Split scoring: Haiku for C1/C2/C5 (factual); Sonnet for C3/C4/C6 (judgment-heavy). |
| MCA NIC code noise too high | High | Accept 60–70% discard rate from MCA data. Supplement with higher-precision sources (DSIR, USFDA, CETP). |
| CETP lists unavailable digitally | Medium | File RTI in Week 1 for key CETP lists. Use MPCB enforcement orders (public documents) to identify chemical companies in CETP zones. |

---

## Tools and Budget

| Tool | Purpose | Cost |
|------|---------|------|
| Claude Haiku API | First-pass ICP scoring (6,000 companies) | ~₹2,700 |
| Claude Sonnet API | Borderline re-scoring (1,200) + hooks (200) | ~₹5,000 |
| Antigravity | MCA NIC code queries | Licence provided |
| Playwright + Python | Website scraping pipeline | Free (open source) |
| GitHub Copilot | Code assistance | Licence provided |
| LinkedIn Sales Navigator | DM discovery | Licence provided |
| Tofler / Zauba Corp | Revenue band and director data for private companies | ~₹5,000 for relevant lookups |
| DSIR PDF parsing | pdfplumber Python library | Free |
| Google Sheets / PostgreSQL | Master data and QA tracking | Free |
| **Total AI + data cost** | | **~₹15,000** |

---

## Final Deliverable Structure

1. **Master CSV** — 1,000 companies: name, website, city, segment, products, revenue band, DM name/title/background, C1–C6 scores with evidence, verdict, confidence flags, source
2. **Priority-200 list** — top 200 by Federer score, with personalization hooks
3. **Tier classification** — Tier 1 (listed, high confidence), Tier 2 (unlisted, AI-verified), Tier 3 (needs phone call first)
4. **Source breakdown** — which source contributed what number and quality of final companies
5. **Scoring pipeline code** — Python scraper, Claude scoring prompt, QA flags, all reproducible

---

## Part B, Question 1: Summary Table

| Sourcing Method | Why It Works for This ICP | Expected Yield | Limitations |
|---|---|---|---|
| DSIR R&D Unit List | Pre-filters for technical seriousness (C3 + C4) | 800–1,000 | Misses new companies; address-only, no website |
| CETP Member Lists | Confirmed chemical/pharma manufacturer (C1) | 400–600 per zone | Requires RTI or MPCB access; 30-day lag |
| USFDA/EU-GMP Facility Lists | Confirms manufacturer + differentiation + export (C1, C3, C5) | 300–500 | Pharma/API heavy; misses performance chemicals |
| BSE SME + MCA NIC Codes | Revenue and ownership data for listed/registered companies | 1,000–1,500 (noisy) | NIC self-reported, often wrong; noisy for unlisted |
| Export Promotion Council Directories | Export-oriented manufacturers (C5 signal) | 500–800 | Biased toward export, misses domestic-focused companies |
| Trade Expo Exhibitor Lists | Growth intent (C6 signal) + segment tagging | 500–700 | Biased toward companies that can afford booth fees |
| LinkedIn Sales Navigator (Inverted) | Find technical founders directly (C4 signal) | 400–600 | Indian MSME founders often absent from LinkedIn |
| Government Scheme Beneficiaries | High-precision: already passed government technical screening | 200–400 | Coverage limited to specific sectors; RTI required |
