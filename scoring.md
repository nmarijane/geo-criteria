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
| S17 | hreflang: skip if monolingual → -2 from max |
| S18-S21 | Core Web Vitals: skip if PageSpeed API fails → -10 from max (3+3+2+2) |
| G16 | FAQPage: skip if no FAQ content → -3 from max |

## SEO and GEO formulas

```
seo_max = 47 - (3 if S10_skipped) - (2 if S17_skipped) - (10 if S18_S21_skipped)
seo_normalized = (seo_points / seo_max) × 100
```

```
geo_max = 61 - (3 if G16_skipped)
geo_per_page_avg = sum(page_geo_scores) / num_pages
geo_points = geo_per_page_avg + G23_points + G24_points + G25_points
geo_normalized = (geo_points / geo_max) × 100
```
