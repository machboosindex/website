# Machboos Index data

Open data behind the Machboos Index (https://machboosindex.pages.dev): restaurant machboos prices and supermarket prices in Kuwait.

## Files

| File | What it holds |
|---|---|
| machboos_prices_talabat_dasma_2026-11-24.csv | Every single-plate chicken and lamb machboos found on restaurant menus, with its price |
| machboos_index_history.csv | The yearly index, 2016 to 2026, with the official price index used to estimate past years |
| grocery_prices_talabat_dasma_2026-11-25.csv | The 40 products compared on the website (13 machboos ingredients and 27 other everyday products), with the price at each store |
| grocery_matched_products_talabat_dasma_2026-11-25.csv | Every product found at five or more of the nine stores (983 products), one column per store |

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

## Supermarket prices

- Date: 25 November 2026.
- Source: each store's grocery listing on Talabat, with Dasma chosen as the delivery area.
- Stores (9): LuLu Hypermarket, Sultan Center, City Hypermarket, Grand Hyper, Monoprix, Talabat Mart, Adailiya Co-op, Rumaithiya Co-op, Surra Co-op.
- Read: the everyday food and drink shelves of each store (dairy, eggs, rice, sugar, oil, flour, bread, canned food, chicken, water, tea, spices, cooking sauces, dried fruit, fresh vegetables and similar), 16,847 product listings in total.

### How products are matched

Two listings count as the same product only when they carry the same barcode. Names are not used for matching, so a 1 L carton is never compared with a 2 L carton, or one brand with another.

The website compares 40 products: 13 ingredients for a chicken machboos (category `machboos`) and 27 other everyday products (milk, eggs, rice, sugar, flour, bread, water, tea and similar). They were chosen by hand from the products that most stores list. A store with no price for a product does not list that barcode.

### Machboos ingredients

The basket on the website starts with 13 ingredients for a chicken machboos: whole chicken, basmati rice, tomato paste, sunflower oil, salt, dried lime (loomi) powder, black pepper, turmeric, cardamom, cinnamon, cloves, mixed chicken spices and coriander seeds.

- For each ingredient, one brand and pack size was chosen so that as many stores as possible list every item. Four stores list all 13: LuLu Hypermarket, City Hypermarket, Monoprix and Talabat Mart. The other five are missing at least three of them, so their basket total is not compared.
- A store that sells a different brand or pack size of an ingredient is treated as not listing it.
- Fresh onions, garlic and tomatoes are left out. Stores sell them loose under their own codes, so no barcode is shared between stores.

### Things to know

- `price_kd` is the price shown on the day. `regular_price_kd` is the price before any offer. 25 of the 290 prices were on offer that day, and the website uses the price shown.
- These are delivery-listing prices. Prices inside the store can differ.
- A few prices look unusual (for example one store lists the 5 kg Tilda rice at 6.195 KD while others list 3.660). They are kept as listed.
- Other large chains that do not deliver groceries to Dasma on Talabat are not covered.

### Columns in grocery_prices_talabat_dasma_2026-11-25.csv

| Column | Meaning |
|---|---|
| date_collected | Day the listing was read |
| source, delivery_area | Where the listing was read and the delivery area chosen |
| barcode | The product barcode used for matching |
| product, brand, size, category | The product as named on the website |
| store | Store name |
| price_kd | Price shown on the day, in KD |
| regular_price_kd | Price before any offer, in KD |
| in_stock | yes if the store showed the product as available |
| title_on_listing | The product name as the store wrote it |

### Columns in grocery_matched_products_talabat_dasma_2026-11-25.csv

| Column | Meaning |
|---|---|
| date_collected | Day the listing was read |
| barcode | The product barcode used for matching |
| subcategory | The shelf the product was listed under |
| title | The product name on one of the listings |
| stores_listing | How many of the nine stores list this barcode |
| lulu_kd ... surra_kd | Price shown at each store, in KD. Empty means the store does not list it |
