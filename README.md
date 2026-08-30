# Journal-Entry-Testing-Anomaly-Detection

The Problem

Journal entry testing during audit fieldwork is typically performed on a sample — a statistically selected slice of the transaction population, because manually reviewing every entry isn't practical at scale. The consequence is that the quality of the review depends entirely on the luck of the sample: if a risky entry falls outside the selected set, it simply never gets looked at.

This creates a real audit-risk gap. Duplicate payments, entries with mismatched purchase order and invoice amounts, postings made outside normal business hours, and approvals lacking proper segregation of duties can all sit undetected in the unsampled majority of a transaction population.

What Was Identified

Reviewing how audit teams currently approach journal entry testing surfaced three recurring gaps:

Coverage gap — sampling by design leaves most of the population untested.

Detection gap — manual review only catches the red flags a reviewer thinks to check for; anything outside known patterns goes unnoticed.

Prioritization gap — even within a sample, every entry gets roughly equal attention, rather than review time being directed at the entries most likely to be problematic.
How It Was Solved

A screening approach was built to test the entire transaction population, not a sample, using two layers of detection working together:

Known-pattern testing — the standard checks audit teams already rely on: duplicate payments, purchase order/invoice/payment mismatches, weekend or after-hours postings, suspiciously round amounts, and preparer/approver segregation-of-duties violations.

Pattern-anomaly testing — a statistical model that flags transactions behaving unusually relative to their vendor's typical amount, timing, and frequency, catching irregularities that don't match any predefined rule.

Each transaction is then assigned a composite risk score and placed into one of four tiers — Critical, High, Medium, Low — so review effort is directed by risk rather than spread evenly or left to sampling chance. Transactions flagged by both layers land in the Critical tier, since agreement between a known-pattern test and an independent anomaly signal is the strongest indicator of a genuine issue.

The output is delivered as a decision-ready dashboard, built for how an audit manager actually works: a population-level risk overview, a view of where both detection layers agree, a vendor-level risk ranking, and a transaction-level detail view showing exactly why each entry was flagged.

Results

Tested against a transaction population with known anomalies deliberately included (to allow the approach to be validated against ground truth, which real audit populations don't provide):

Metric	Result
Anomalies identified	98%
False positives on clean transactions	3%
Categories with full detection	Duplicate payments, weekend postings, odd-hour postings, round-number amounts, PO/invoice/payment mismatches, segregation-of-duties violations
Hardest category	Unusual-amount outliers (85% detection — a matter of degree rather than a fixed rule)

Recommendations

Route Critical and High-tier transactions to manual review first, rather than testing a random sample — this concentrates the highest-cost activity (auditor time) on the highest-likelihood issues.

Treat vendor-level risk ranking as an input to engagement planning — vendors that consistently surface in the Vendor Drill-down view warrant closer scrutiny in future testing cycles, not just the current one.

Use agreement between the two detection layers as a confidence signal — when a known-pattern rule and the anomaly model both flag the same transaction, that agreement itself is meaningful and should weight review priority more than either signal alone.

Revisit the anomaly threshold periodically — the model assumes roughly 4% of a population is anomalous; this should be recalibrated against actual findings over a few testing cycles rather than treated as fixed.
