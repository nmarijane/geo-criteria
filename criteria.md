# Criteria

Every row below is a single, independently checked condition — binary: it either passes or it fails, never partial credit. Severity marks how much a failed check weighs in the overall score, and pass condition is the exact rule applied. Impact / rationale, where a figure exists, is a citation-impact number from published research, not from our own measurement — see the note below the GEO table for the primary source; where no figure exists, the column states the qualitative reason the check matters instead.

## SEO criteria

| ID | Criterion | Severity | Pass condition |
| --- | --- | --- | --- |
| S1 | Title tag | HIGH | ≤60 chars AND keyword in first 3 words |
| S2 | Meta description | HIGH | Present AND 120-160 chars |
| S3 | URL / slug | MEDIUM | <60 chars, no stopwords, contains keyword |
| S4 | H1 unique | HIGH | Exactly 1 H1 per page |
| S5 | H2/H3 structure | MEDIUM | ≥4 H2, no hierarchy skips (H1→H3) |
| S6 | Keyword in first 100 words | MEDIUM | ≥1 keyword from title in opening text |
| S7 | Word count | LOW | ≥1500 words for long-form content |
| S8 | Internal links | HIGH | ≥2 internal links in content body |
| S9 | External links | MEDIUM | ≥3 links to authoritative external sources |
| S10 | Broken links | HIGH | 0 links returning 404/5xx |
| S11 | Canonical URL | MEDIUM | Present and matching current URL |
| S12 | Descriptive anchors | LOW | No "click here" / "read more" anchors |
| S13 | Crawlable links | MEDIUM | No javascript:void(0), no empty href |
| S14 | Image alt text | MEDIUM | All content images have descriptive alt (≥3 words) |
| S15 | Open Graph tags | LOW | og:title, og:description, og:image all present |
| S16 | No accidental noindex | HIGH | No unintended noindex directive |
| S17 | Hreflang | MEDIUM | Valid hreflang if multilingual; skip if monolingual |
| S18 | Lighthouse Performance | HIGH | Score ≥ 90 (mobile) |
| S19 | LCP (Largest Contentful Paint) | HIGH | ≤ 2500ms |
| S20 | CLS (Cumulative Layout Shift) | MEDIUM | ≤ 0.1 |
| S21 | TBT (Total Blocking Time) | MEDIUM | ≤ 200ms |

## GEO criteria

G23, G24, and G25 are evaluated once for the entire site, not per page — every other criterion in this table is checked separately on each page.

| ID | Criterion | Severity | Pass condition | Impact / rationale |
| --- | --- | --- | --- | --- |
| G1 | Answer Blocks | HIGH | ≥2 H2 as questions with self-contained 2-3 sentence answers | **+27% AI visibility** |
| G2 | Modular structure (Ranch-Style) | HIGH | Zero cross-references ("as mentioned above", "see below") | Sections with cross-refs get ignored |
| G3 | Factual tables | MEDIUM | ≥1 table with numeric/comparative data | LLMs prefer structured data |
| G4 | Answer-First (200 words) | HIGH | First 200 words directly address title topic with ≥2 keywords | **55% of citations from first 30%** |
| G5 | Citable capsules | HIGH | ≥50% of H2 sections open with 40-60 word autonomous paragraph | **2.3× more citations** |
| G6 | Short paragraphs | LOW | Avg ≤4 sentences/paragraph, <10% over 5 sentences | Improves LLM extraction |
| G7 | Attributed statistics | HIGH | ≥3 stats with named source within 50 words | **+40% AI visibility** |
| G8 | Stats cadence | MEDIUM | 1 stat per 150-200 words | Optimal credibility density |
| G9 | Credible source citations | HIGH | ≥2 recognized institutions cited (universities, analysts, gov) | **+115% AI visibility** |
| G10 | Named expert quotes | HIGH | ≥1 direct quote with name + credentials in quotes | **+41% — best single factor** |
| G11 | Attribution language | MEDIUM | ≥3 "according to" / "research shows" expressions | **+40% AI visibility** |
| G12 | No promotional language | MEDIUM | Zero instances of: revolutionary, industry-leading, game-changer, best-in-class, cutting-edge, disruptif, leader du marché, inégalé, numéro 1, #1 (English and French equivalents) | Reduces LLM trust |
| G13 | JSON-LD Article/BlogPosting | HIGH | Schema present with mainEntityOfPage, headline, description | — |
| G14 | Author knowsAbout + sameAs | HIGH | Author schema has expertise domains + ≥1 verifiable profile link | — |
| G15 | dateModified | HIGH | Present in JSON-LD AND ≥ datePublished | — |
| G16 | FAQPage schema (nested) | HIGH | If FAQ content exists → FAQPage nested in Article schema. Skip if no FAQ. | — |
| G17 | Connected entities (@graph) | LOW | ≥2 entity types linked via @graph | — |
| G18 | Content freshness | MEDIUM | Last modified < 90 days | **76% of Perplexity citations from content < 30 days** |
| G19 | Dated statistics | MEDIUM | No stats > 12 months presented as current without year qualifier | **65% of AI citations from sources < 1 year** |
| G20 | Query fan-out | MEDIUM | ≥3 sub-intents covered (what, why, how, how much, when, for whom, vs alternatives) | — |
| G21 | Explicit definitions | LOW | ≥50% of technical terms defined at first use | — |
| G22 | Consistent terminology | MEDIUM | Key concepts use one consistent term throughout (after optional first-mention synonym) | — |
| G23 | AI crawlers allowed | HIGH | robots.txt allows GPTBot, OAI-SearchBot, ChatGPT-User, ClaudeBot, PerplexityBot, CCBot, anthropic-ai | **0 citations if blocked** |
| G24 | SSR / HTML content | HIGH | >100 words of content in raw HTML without JavaScript execution | AI crawlers don't execute JS |
| G25 | Organization sameAs (brand entity) | HIGH | Organization JSON-LD present with ≥1 sameAs link to an official brand profile | Brand entity resolution & trust for AI + Knowledge Graph |

Most of the impact figures above are drawn from published research, not from in-house measurement. The primary source is Princeton/ACM SIGKDD 2024 research on AI citation optimization; a few criteria draw on other published research instead of this one.

## Recommendations

These are not scored checks — they are additions that help an AI answer engine understand a page better. What to add, and why it helps, is listed below.

| ID | What | Why |
| --- | --- | --- |
| R1 | llms.txt at site root | Semantic robots.txt for AI — emerging standard, now also checked by Lighthouse's agentic-browsing category. |
| R2 | HowTo schema | If procedural content exists, helps AI extract steps |
| R3 | BreadcrumbList schema | Helps AI understand site hierarchy |
| R4 | Speakable schema | Identifies key passages for voice AI assistants |
