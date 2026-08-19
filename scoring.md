# Scoring

How the pass/fail results from `criteria.md` turn into a single score: point values per severity, how SEO and GEO combine, the grade bands, and when a criterion is skipped instead of counted as a fail.

## Points

Every criterion is binary — it either passes or it fails, no partial credit. A pass earns points based on its severity; a fail earns zero.

| Severity | Points on pass |
| --- | --- |
| HIGH | 3 |
| MEDIUM | 2 |
| LOW | 1 |

## Weighting

The overall score blends the SEO score and the GEO score: SEO counts for 40%, GEO for 60%. GEO carries the larger share because AI-citation readiness is the differentiator — basic SEO is table stakes.

```
score = round(seo_normalized × 0.40 + geo_normalized × 0.60)
```

## Grade

| Score | Grade | Label |
| --- | --- | --- |
| 85-100 | A | Excellent |
| 70-84 | B | Good |
| 50-69 | C | Average |
| 30-49 | D | Weak |
| 0-29 | F | Critical |

## Skip rules

A criterion that can't be evaluated — a request that times out, a check whose precondition doesn't hold — is skipped: removed from both the score's numerator and its denominator, rather than counted as a fail.

| Criterion | Condition |
| --- | --- |
| S10 | broken links: skip if unreachable → -3 from max |
| S14 | image alt text: skip if the page has no content images → -2 from max |
| S17 | hreflang: skip if monolingual → -2 from max |
| S18-S21 | Core Web Vitals: skip if PageSpeed API fails → -10 from max (3+3+2+2) |
| G5 | citable capsules: skip if the page has under 100 words, or no H2 → -3 from max |
| G14 | author schema: skip if the page carries no Article schema → -3 from max |
| G15 | dateModified: skip if the page carries no Article schema → -3 from max |
| G16 | FAQPage: skip if no FAQ content → -3 from max |
| G19 | dated statistics: skip if the page states no statistics at all → -2 from max |

## Applicability by page type

Each crawled page is classified, and criteria that make no sense for that kind of page are treated as inapplicable — skipped, so they lower the maximum instead of counting as failures. The matrix is deliberately conservative: a criterion is only switched off where the expectation would be indefensible (sourced statistics on a hotel room listing), never merely because it is less important. The site-global criteria are never inapplicable.

| Page type | Criteria not applicable |
| --- | --- |
| editorial | none — every criterion applies |
| unknown | none — every criterion applies |
| home | G7, G8, G10, G13, G14, G18, G19 |
| transactional | G7, G8, G9, G10, G11, G13, G14, G15, G18, G19 |
| institutional | G7, G8, G9, G10, G11, G13, G14, G15, G18, G19 |
| listing | G1, G4, G5, G7, G8, G9, G10, G11, G14, G15, G18, G19, G20, G21 |

## SEO and GEO formulas

```
seo_max = 47 - (points of every skipped SEO criterion)
        = 47 - (3 if S10) - (2 if S14) - (2 if S17) - (10 if S18-S21)
seo_normalized = (seo_points / seo_max) × 100
```

```
geo_max = 61 - (points of every skipped GEO criterion)
        = 61 - (3 if G5) - (3 if G14) - (3 if G15) - (3 if G16) - (2 if G19)
              - (points of criteria the page type makes inapplicable)
geo_per_page_avg = sum(page_geo_scores) / num_pages
geo_points = geo_per_page_avg + G23_points + G24_points + G25_points
geo_normalized = (geo_points / geo_max) × 100
```
