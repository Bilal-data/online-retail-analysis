# online-retail-analysis
Revenue analysis of a UK online retailer (UCI Online Retail dataset)


Analysis of the transactions of a UK-based online retailer (1 Dec 2010 to 9 Dec 2011), done with Python (pandas) in Google Colab.

## Data

- UCI Machine Learning Repository, [Online Retail](https://archive.ics.uci.edu/dataset/352/online+retail): 541,909 rows, 8 columns.
- License: CC BY 4.0. Citation: Chen, D. (2015). Online Retail [Dataset]. UCI Machine Learning Repository. https://doi.org/10.24432/C5BW33
- The data file is not included here. The notebook downloads it from UCI.

## Cleaning decisions

- 135,080 rows (about 25%) have no CustomerID and 1,454 have no Description.
- 10,624 rows have a negative quantity. 9,288 of them are cancellations (the invoice number starts with C). The other 1,336 have a unit price of 0 and no description or customer. They look like stock adjustments, but the data does not say.
- Gross view: only rows with quantity and price above 0 (530,104 rows, 11,805 removed).
- Net view: all rows with price above 0, so returns and cancellations are subtracted.

## Key findings

- UK customers bring 84.6% of gross revenue. Next: Netherlands 2.7%, EIRE 2.7%, Germany 2.1%, France 2.0%.
- Monthly net revenue peaks in November 2011 (1,461,756). September to November are far above the earlier months (about 0.5 to 0.75 million).
- The data ends on 9 Dec 2011 at 12:50, so December 2011 is incomplete. Comparing it with a full month is misleading.
- Same-period check (1 to 9 December): gross revenue looks 45.6% higher in 2011 (438,853 against 638,793). But one invoice (581483, 80,995 units of a single item, 168,470) was cancelled 12 minutes later (C581484). On a net basis the growth is 14.9% (377,488 against 433,668). Invoice counts were almost the same (834 and 819).

## Limitations

- Descriptive analysis only. I have not run a statistical test yet.
- The 14.9% comes from 9 days only, so it is a hint, not a conclusion.
- Customer-level analysis would cover only about 75% of rows (the ones with a CustomerID).
- I matched only one cancellation to its original invoice. Other cancellations may refer to earlier sales that I did not check.
- The net view still includes non-product lines such as discounts, because I only filtered on price.
- No cost or profit column, so this is revenue only. The data does not state the currency.
