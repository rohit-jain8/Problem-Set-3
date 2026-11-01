# ECON 3916 — Problem Set 3: The Number Nobody Can Reproduce

This problem set examines how SQL queries can produce misleading results and how to check those results before using them in a report. It also explores the difference between correlation and causation using simulated customer data.

## What I Did

### Phase 1 — Reproducing the Revenue Numbers
I created `customers` and `orders` tables in DuckDB and compared average revenue for West-region customers before and after joining the tables. The correct customer-level average was 810.65, while the joined query returned 1,246.41 because customers with more orders were counted multiple times. I also created a simple check to flag joins that increase row counts.

### Phase 2 — Missing Values
I set 15% of customer regions to missing and showed how `WHERE region != 'West'` excludes those customers. Adding `OR region IS NULL` recovered 450 rows. I then used a window function to show each customer's revenue alongside their region's average without changing the total of 3,000 customer rows.

### Phase 3 — Causal Analysis
I simulated an account-management programme with a known revenue effect of 20. A naive comparison estimated 335.45, while adjusting for existing account size brought the estimate to 22.57. Adding support tickets as a control moved the estimate to -72.47, showing how an inappropriate control can make an estimate less accurate. These are simulation results, not evidence of the programme's real-world impact.

### Phase 4 — SQL Reviewer
With AI assistance, I developed and tested a `review_query(con, sql)` function that returns warnings about row-count increases after joins, missing-value filters, and potentially misleading aggregates. The notebook includes an evaluation of what the reviewer catches and misses, an AI transcript, and a short report to the director.

## Tools Used
- Python and Google Colab
- DuckDB and SQL
- pandas and NumPy

## Files
- `Econ_3916_PS3.ipynb` — Code, query results, explanations, AI transcript, and final writeup

## Main Takeaway
Before reporting a number, it is important to check what each row represents, whether joins duplicate records, how missing values are handled, and whether a comparison supports a causal conclusion.
