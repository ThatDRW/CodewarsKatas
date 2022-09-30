# 7 kyu - Grocery Store Real Price
## Instructions
You are the owner of the Grocery Store. All your products are in the database, that you have created after CodeWars SQL exercises! :)

Customer often need to now how much really they pay for the products. Manufacturers make different sizes of same product so it is hard to compare prices, sometimes they make packages look big, but the weight of the product is small.

Make a SELECT query which will tell the price per kg of the product.

Weight is in grams! Round the price_per_kg to 2 decimal places.

Order results by price_per_kg ascending, then by name ascending.
Products table schema:

    id (int)
    name (string)
    price (float)
    stock (int)
    weight (float)
    producer (string)
    country (string)

Results table schema:

    name (string)
    weight (float)
    price (float)
    price_per_kg (float)

## Examples
```

```

## My Solution #1 - 
```sql
SELECT    name,
          weight,
          price,
          CAST(ROUND(CAST(1/(weight/1000)*price as dec) , 2) as float) AS price_per_kg
FROM      products
ORDER BY  price_per_kg ASC, name ASC
```