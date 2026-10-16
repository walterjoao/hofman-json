# hofman-json

Product catalogue data for Hofman Animal Care (horse, pet and farm supplies), stored as JSON and ready to import into a shop.

## Files

| File | Contents |
|---|---|
| `products.json` | 4,833 products |
| `produ.json` | Same data as `products.json` (identical when parsed; only the formatting differs) |

## Data model

Each product is an object with:

| Field | Description |
|---|---|
| `handle` | URL slug, e.g. `veip-actisept-plus-5-l` |
| `title` | Product name |
| `vendor` | Brand (227 distinct vendors) |
| `product_type` | Original Dutch category, e.g. `Paard - Stal en weide` |
| `product_type_pt` | Portuguese category, e.g. `Cavalo - Estábulo e Pasto` (125 distinct types) |
| `body_html` | Description (Dutch HTML/text) |
| `published` | `"TRUE"` / `"FALSE"` |
| `variant_type` | Kind of variant, e.g. `size` |
| `tables` | Related rows, each with a `table` discriminator (see below) |

`tables` entries:

- `main_image`: `position`, `src`
- `image`: additional product images
- `variant`: `option_name`, `option_value`, `price`, `stock`
- `google_shopping_attribute`: `key`, `value` (e.g. Gender, Age Group, Condition)

The layout mirrors Shopify-style product exports (handle, vendor, product type, variants, images), so it maps easily onto a CSV or API import.

## Usage

```python
import json

with open("products.json", encoding="utf-8") as f:
    products = json.load(f)

print(len(products), products[0]["title"])
```

Images point to `api-prod.hofmananimalcare.nl`; check you have the right to use the content before republishing it.
