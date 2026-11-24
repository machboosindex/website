# Machboos Index data

Open data behind the Machboos Index (https://machboosindex.pages.dev).

## Files

| File | What it holds |
|---|---|
| machboos_prices_talabat_dasma_2026-11-24.csv | Every single-plate chicken and lamb machboos found on restaurant menus, with its price |
| machboos_index_history.csv | The yearly index, 2016 to 2026, with the official price index used to estimate past years |

## How the prices were collected

- Date: 24 November 2026.
- Source: restaurant menus on Talabat, with Dasma chosen as the delivery area.
- Scope: the 173 restaurants listed under the Kuwaiti and Machbouss cuisines. 108 of them had a machboos dish.
- Kept: single-person plates of chicken machboos and lamb (meat) machboos.
- Left out: family trays, platters, combos and offers, kids' meals, rice-only orders, and other meats (fish, shrimp, duck, pigeon, camel).
- 37 dishes show their price only after a size is chosen. They are listed without a price and are not used.

Delivery-app menu prices can be higher than dine-in prices at the same restaurant.

## How the index is calculated

1. One price per kitchen and dish: its lowest-priced standard plate (`used_in_index = yes`).
2. Restaurants that share the same menu and prices are counted once (`kitchen_group`).
3. If a dish was discounted on the day, the regular price is used (`list_price_kd`).
4. The index is the median of those prices. Budget and premium are the medians of the cheapest tenth and the most expensive tenth of restaurants.

| Dish | Restaurants | Budget (cheapest tenth) | Median | Premium (most expensive tenth) |
|---|---|---|---|---|
| Chicken machboos | 80 | 2.500 | 3.000 | 4.350 |
| Lamb machboos | 64 | 4.000 | 5.000 | 6.800 |
| Lamb machboos, Australian lamb | 22 | | 4.750 | |
| Lamb machboos, Arabic (Naimi) lamb | 24 | | 6.375 | |

Prices are in Kuwaiti dinars.

## History before 2026

Old menu prices could not be recovered, so earlier years are estimates:
the 2026 median multiplied by (that period's index / the 2026 index), using the
Restaurants and Hotels consumer price index (2013 = 100) published by Kuwait's
Central Statistical Bureau and republished by the Central Bank of Kuwait.

- 2016 to 2022: official yearly values.
- 2023 to 2025: approximated from published monthly figures.
- 2026: the official mid-year value (137.0).

On the website's chart, each yearly value sits at mid-year and the months in between are interpolated.

This index covers all restaurants and hotels, not machboos alone, so the estimated history is a guide, not a record.

## Columns in the price file

| Column | Meaning |
|---|---|
| date_collected | Day the menu was read |
| source, delivery_area | Where the menu was read and the delivery area chosen |
| restaurant, talabat_branch_id | Restaurant name and its branch number on Talabat |
| kitchen_group | Restaurants with the same menu share one group name |
| dish | chicken or lamb |
| meat_origin | For lamb: arabic, australian, or unspecified |
| item_name | The dish name on the menu |
| list_price_kd | Regular price in KD |
| price_shown_kd | Price shown on the day, after any discount |
| used_in_index | yes if this is the price counted for the restaurant and dish |
| used_in_origin_median | yes if counted in the Australian or Arabic lamb median |
| note | Why a row was not counted, where that applies |
