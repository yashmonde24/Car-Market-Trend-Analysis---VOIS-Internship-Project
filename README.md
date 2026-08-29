## Car Market Trend Analysis

1. Background and Overview

Used-car prices get thrown around based on gut feel - "diesel resells better," "low mileage means high price," "avoid second-owner cars." Some of that is true. Some of it isn't. This project pulls 301 real CarDekho listings and checks which factors actually move resale price and by how much, instead of going on instinct.

2. Data Structure Overview
- 301 rows, 9 original columns - car name, year, selling price, present price, kms driven, fuel type, seller type, transmission, owner count
- 299 rows after cleanup — 2 duplicates removed, 0 missing values otherwise
- 5 engineered fields added on top: Car Age, Depreciation Amount, Depreciation % and Mileage Bucket (0–25k / 25k–50k / 50k–75k / 75k–100k / 100k+ km)
- No messy nulls to fight here - the real work was in the feature engineering and reading the trends correctly.

3. Executive Summary
- Present Price is the single best predictor of what a car actually resells for (correlation 0.80)
- Fuel type and who's selling the car matter more than raw mileage.
- Diesel cars sell for over 2x what Petrol/CNG cars do.
- Dealer listings sell for roughly 10x what individual sellers get.
- Mileage's effect is real but not linear - it barely correlates with price directly, but depreciation climbs steadily as mileage buckets go up.
- Most cars are priced modestly - median selling price is ₹3.6L well below the ₹4.66L average which a few expensive listings are dragging up.

4. Insights Deep Dive

- Present Price drives Selling Price. Correlation of 0.80 - the strongest relationship in the dataset. Any pricing logic should start here, not with age or    mileage.

- Diesel commands a real premium. Average ₹6.9L vs ~₹3.0–3.1L for Petrol and CNG. Worth noting: there are no diesel automatics in this data, so this reads as a fuel-type effect, not a transmission one.

- Seller type is the sharpest split in the whole dataset. Dealer median ₹4.98L vs Individual median ₹0.51L. That's not really a "dealers charge more" story — it's more likely dealers are simply carrying newer, better-kept stock.

- Mileage doesn't behave the way you'd expect. Raw Kms Driven vs Selling Price correlation is basically zero. But when you bucket mileage into ranges, depreciation rises steadily from the 0–25k bracket to the 75k–100k bracket. The relationship exists — it's just not a straight line, so it won't show up if you only check a simple correlation.

- Car age follows the depreciation curve you'd expect — steep value loss in the early years, tapering off later. Past ~15 years, the trend gets noisy because there just aren't many listings that old to average over.

- Ownership history has a visible penalty, but tread carefully: 96.3% of listings have zero previous owners, and the "3 owners" group is a single car. That last data point isn't a trend, it's an outlier with a sample size of one.

5. Recommendations
- Use Present Price as the anchor variable in any pricing or valuation model — it carries the most signal.
- Price by mileage bucket, not raw kilometers - a linear model will miss the real relationship.
- Treat fuel type and seller type as separate pricing tiers, not features to average across.
- Benchmark against median price, not mean - the mean is skewed by a small number of high-value listings.
- Don't build age-based pricing rules past ~15 years old without collecting more data first — the current sample is too thin there.

6. Assumptions and Limitations
- 299 rows is a small dataset — some subgroups (CNG cars, diesel automatics, 3-owner cars) barely exist, so those splits aren't statistically solid.
-Everything here is correlation, not causation — "dealer" and "diesel" price premiums likely bundle in other quality factors that weren't captured directly.
- One outlier at 500,000 km distorts the raw mileage-price scatterplot; bucketed mileage is the safer way to read that relationship.
- This is a directional analysis for decision-support, not a production-ready valuation model.

7. Future Enhancements
-Bring in more records to properly test the thin subgroups (diesel automatics, high-mileage cars, multi-owner cars).
- Add a proper regression or ML model now that the key predictors are identified, rather than relying on correlation alone.
- Pull in brand/model-tier data — "Car_Name" wasn't used in this pass, and it likely explains some of what's currently attributed to seller type.
- Track price over time (if repeat listings become available) to separate genuine depreciation from one-off pricing decisions.

8. Deliverables
- Car_Market_Trend_Analysis.ipynb — full analysis notebook (data cleaning, feature engineering, EDA, charts).
- Car_Market_Trend_Analysis.pptx — presentation deck summarizing findings for a non-technical audience.

9. Output Demo
  Link : https://github.com/yashmonde24/Car-Market-Trend-Analysis---VOIS-Internship-Project/tree/main/output

