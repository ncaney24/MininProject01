## Cleaning Decisions Log

Here's a summary of the main judgment calls made during cleaning and why.

**1. Encoding — ISO-8859-1**
The file wouldn't load with default UTF-8 because of the £ symbol.
Switched to ISO-8859-1 and it worked fine.

**2. Kept raw untouched**
All cleaning was done on df = raw.copy(). Kept raw as-is throughout
so we can always go back and check anything against the original.

**3. Dropped blank descriptions (~1,454 rows)**
No way to figure out what product these rows refer to, and they're
only 0.3% of the data so dropping them doesn't really hurt anything.

**4. Removed cancellations (~9,288 rows)**
InvoiceNo starting with 'C' flags a cancellation in this system.
These are reversals of previous sales, not actual revenue, so they
need to come out before any revenue calculation.

**5. Removed non-product StockCodes (~750 rows)**
Codes like POST, DOT, AMAZONFEE, BANK CHARGES are admin/fee entries.
Including them would mess up product-level analysis and inflate revenue.

**6. Removed Quantity <= 0 (~10,624 rows)**
Negative quantities are returns. Zero quantities contribute nothing.
Both need to go.

**7. Removed UnitPrice <= 0 (~40 rows)**
A price of zero or below isn't a real sale. Checked a few of these
manually and they looked like test entries or data errors.

**8. Dropped exact duplicates (~5,268 rows)**
All columns identical — almost certainly a double-export from the
source system. Keeping them would double-count those transactions.

**9. Filled missing CustomerID with 'UNKNOWN' (~135,080 rows)**
Dropping 25% of the dataset felt too aggressive when those rows still
have perfectly good product and revenue data. Went with 'UNKNOWN' as
a sentinel and just excluded them from customer-level metrics.

**10. Standardised country labels**
EIRE → Ireland, RSA → South Africa, Unspecified → NaN.
These are just inconsistent labels for the same places — needed to
fix them before the region merge would work properly.

**11. Dropped stock_code after 3.12**
stock_code was only needed to filter out the non-product entries.
Once that was done, every business question in Part 2 works off
description, country, customer_id, or time — so stock_code
wasn't needed anymore.