# Kenya Food Market Prices Analysis

An analysis of 14 years (2006 to 2019) of real WFP maize and bean prices, prepared for **Pamoja Agri-Advisory** (a fictional Kenyan NGO). It answers two questions:

1. Should smallholder farmers sell maize at harvest, or store it and sell later?
2. Which retail markets cost households the most?

All code and outputs are in [`analysis.ipynb`](analysis.ipynb).

## Data

| Item | Detail |
|---|---|
| File | `data/food-prices-kenya.csv` (2,742 rows, 9 columns; 11 after adding `year` and `month`) |
| Source | WFP Kenya Food Prices, via the Humanitarian Data Exchange (HDX) |
| Licence | CC BY-IGO 3.0 |
| Period | 15 January 2006 to 15 December 2019 (monthly) |
| Commodities | White maize and dry beans |
| Wholesale prices | KES per 90 KG bag: Nairobi, Mombasa, Kisumu, Eldoret, Nakuru |
| Retail prices | KES per KG: Garissa, Hola, Kajiado, Kilifi, Kitui, Lodwar, Mandera, Marigat, Marsabit |

The data is not included in this repository. Place the CSV in a `data/` folder next to the notebook.

## How the analysis is organised

The notebook follows five tasks in order.

1. **Load and clean.** Converted `date` to real dates, added `year` and `month`, and filled the missing county and region for Hola (59 rows) with Tana River and Coast. After the fill, no missing counties remain, and there are no duplicate rows.
2. **Compare like with like.** Split the data into wholesale (`df_wholesale`, 90 KG) and retail (`df_retail`, KG) and never averaged them together. Added `price_per_kg` (wholesale price divided by 90, retail unchanged).
3. **Maize prices over the years.** Average wholesale maize price per bag by year, with the year-on-year change in KES, plus a line chart.
4. **Sell at harvest or hold?** Average wholesale maize price by month, then a January vs June comparison for each market and year, plus a line chart, a boxplot and a violin plot of prices by market.
5. **Where households pay most.** Average retail maize price per market for 2015 to 2019, ranked within each year.

## Key results

### Wholesale vs retail maize (per KG)

| Price type | Average (KES per KG) |
|---|---|
| Wholesale | 28.54 |
| Retail | 47.92 |

Retail is about 1.7 times the wholesale price per KG. This is a rough comparison, because wholesale and retail markets are different places and most retail markets only start in 2015.

### Yearly wholesale maize price (KES per 90 KG bag)

- **Highest average year:** 2017 (about 3,744 KES)
- **Biggest rise:** 2011, up about 1,246 KES on 2010
- **Biggest fall:** 2018, down about 1,335 KES on 2017

### When to sell

- **Cheapest month:** January, about 25.88 KES per KG (roughly 2,330 KES per bag)
- **Dearest month:** June, about 31.55 KES per KG (roughly 2,840 KES per bag)
- **Hold January to June:** June was higher than January in **73.3%** of 60 market-years, with a **median gain of 356 KES per bag**.
- **Holding is not risk-free.** In 2010 and 2018 every wholesale market lost money by waiting, and several markets lost in 2007 and 2016.

### Where households pay most (retail maize, 2015 to 2019)

| Market | Average (KES per KG) |
|---|---|
| Lodwar | 75.85 (most expensive) |
| Mandera | 67.53 |
| Garissa | 59.73 |
| Kajiado | 50.88 |
| Hola | 49.87 |
| Marsabit | 47.50 |
| Marigat | 46.53 |
| Kilifi | 43.84 |
| Kitui | 36.19 (cheapest) |

- **Top three in all five years:** Lodwar and Mandera.
- **Garissa** was in the top three in four of five years (it was 4th in 2017).
- **Kajiado** reached the top three only once (2017).
- In 2019, Mandera overtook Lodwar as the dearest market (76.73 KES per KG, against Lodwar's 64.83).

## Recommendations

**For farmer groups**

1. Do not sell everything straight after harvest. Prices are lowest in January and highest in June, and holding paid off in 73.3% of market-years.
2. Expect a modest gain, not a windfall. The median gain was 356 KES per bag, so compare it with your storage costs first.
3. Split your sales: sell some at harvest to meet immediate needs and store the rest. Holding lost money in about 27% of market-years, including every market in 2010 and 2018.

**For county officers**

4. Prioritise Lodwar and Mandera, where households paid the most in every year from 2015 to 2019, and monitor Garissa.

## Limitations

- **Storage costs and risks are not in the calculation.** The January to June gain ignores pests (weevils and rats), theft and fire, quality loss, the need for cash during the storage period, and the cost of bags, rent and treatment.
- **Wholesale and retail are different markets.** The seasonal pattern comes from five wholesale towns and may not apply to retail county towns such as Lodwar.
- **Retail coverage is short.** Five of the nine retail markets only start in 2015, so the retail comparison covers 2015 to 2019 only.
- **Nakuru starts in 2015.** Yearly wholesale averages include five markets from 2015 and four before.
- **Missing prices were dropped.** Market-years without both a January and a June price (for example Kisumu 2008) are excluded from the hold-or-sell comparison.
- **The data ends in 2019.** WFP changed its market list after 2019, so later years are not comparable.

## How to run

Requirements: Python 3, `pandas`, `numpy`, `matplotlib`, `seaborn`, and Jupyter.

```bash
pip install pandas numpy matplotlib seaborn jupyter
jupyter notebook analysis.ipynb
```

The first code cell reads the CSV from a local Windows path. Change it to a relative path before running:

```python
df = pd.read_csv("data/food-prices-kenya.csv")
```

Then choose **Restart and Run All** so every cell runs in order.

## Data credit

Data: WFP Kenya Food Prices, World Food Programme, via the Humanitarian Data Exchange (HDX), licence CC BY-IGO 3.0. Pamoja Agri-Advisory is a fictional organisation; the prices are real.

