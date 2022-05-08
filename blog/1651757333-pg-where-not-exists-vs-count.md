# Postgres where-not-exists ↔ count

Talking about Postgres, here's an interesting scenario where a `SELECT` query, which intuitively should be reasonably fast in a very large table, turns out to be *thousands* times slower than a variation which should instead intuitively be a lot slower.

## Exhibit A

```sql
SELECT *
FROM A
WHERE NOT EXISTS (
    SELECT
    FROM B
    WHERE A.foo = B.foo
)
LIMIT 10000;
```

## Exhibit B

```sql
SELECT *
FROM A
WHERE (
    SELECT COUNT(*)
    FROM B
    WHERE A.foo = B.foo
) = 0
LIMIT 10000;
```

One would assume that exhibit A would be faster than exhibit B, right?

*Nope*.

## Costs

Here's the cost for the first query:

```plain
Limit (cost=5999.xx..xxxxx.xx) rows=10000 width=...)
    -> Merge Anti Join (cost=5999.xx..xxxxxxxxx.xx rows=... width=...)
```

And here's the cost for the second query:

```plain
Limit (cost=0.57..xxxxxxxx.xx rows=10000 width=...)
    -> Index Scan using ... on ... (cost=0.57..xxxxxxxxx.xx rows=... width=...)
```

There might be something weird going on with the DB schema here, but in the real-world version of the snippets above the `foo` columns are both PKs.

I'm not really sure what's going on here - it's probably something silly or trivial (and I'm no PG expert in any way), but the results are quite puzzling.
