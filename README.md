# Kenya Food Market Prices Analysis

Analysis of 14 years of WFP maize price data for **Pamoja Agri-Advisory** (a fictional NGO), answering two questions:

1. Should smallholder farmers sell maize at harvest or store it?
2. Which retail markets cost households the most?

## Data

- **File:** `data/food-prices-kenya.csv` (2,742 rows, 9 columns)
- **Source:** WFP Kenya Food Prices, via the Humanitarian Data Exchange (HDX), licence CC BY-IGO 3.0
- **Coverage:** monthly prices, January 2006 to December 2019
- **Commodities:** white maize and dry beans
- **Price types:** wholesale (KES per 90 KG bag) in 5 town markets; retail (KES per KG) in 9 county markets

## Method

1. **Load and clean:** parsed `date` into real dates, added `year` and `month`, filled Hola's missing county (Tana River) and region (Coast).
2. **Like with like:** split wholesale from retail and never averaged them together. Added `price_per_kg` (wholesale price divided by 90; retail unchanged).
3. **Yearly trend:** average wholesale maize price per bag by year, with year-on-year % change (`groupby` and `pct_change`).
4. **Seasonality:** average wholesale maize price by month, then January vs June per market-year (`pivot_table`).
5. **Retail comparison:** average retail maize price per market for 2015 to 2019, ranked within each year.

## Key findings

**Yearly trend (wholesale maize, per 90 KG bag)**
- Highest average year: [fill in]
- Biggest rise: [fill in]; biggest fall: [fill in]

**When to sell**
- Cheapest month: January (about 25.9 KES/KG, roughly 2,330 KES per bag)
- Dearest month: June (about 31.5 KES/KG, roughly 2,840 KES per bag)
- June was higher than January in **73.3%** of 60 market-years, with a median gain of **356 KES per bag** (about 14%)
- Holding lost money in some years (for example 2010 and 2018), so splitting sales is safer than holding everything

**Where households pay most (retail maize, 2015 to 2019)**
- Most expensive: Lodwar (about 75.85 KES/KG); cheapest: Kitui (about 36.19 KES/KG)
- Top three in every year: Lodwar and Mandera
- Garissa was in the top three in 4 of 5 years and is worth monitoring

## Recommendations

- **Farmer groups:** do not sell everything straight after harvest. Store part of the crop until around June if storage is safe, and sell the rest early to cover immediate needs.
- **County officers:** prioritise Lodwar and Mandera, and monitor Garissa.

## Limitations

- The January to June gain ignores storage costs (bags, pest control, rent), losses to moisture and weevils, theft, and the interest on cash tied up for five months.
- Wholesale (town) and retail (county) markets are different places, so the wholesale seasonal pattern may not apply to retail towns.
- Five of the nine retail markets only start in 2015, so the retail comparison covers 2015 to 2019 only.
- Nakuru only starts in 2015, so yearly wholesale averages include five markets from then on and four before.
- Missing January or June values were dropped from the Jan vs June comparison (for example Kisumu 2008).

## How to run

```bash
pip install pandas numpy matplotlib
python analysis.py
```

Or run the notebook cells top to bottom in the Python Lab. Start with the setup cell, which loads and cleans the data.

## Files

- `data/food-prices-kenya.csv`: input data
- `analysis.py` (or the notebook): all code for Tasks 1 to 5
