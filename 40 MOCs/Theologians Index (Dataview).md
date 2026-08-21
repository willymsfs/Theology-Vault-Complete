---
title: Theologians Index (Dataview)
aliases: [Theologians Index, Who's Who Dataview, People Index]
type: moc
tags: [note/moc, theology, theologians, index]
created: 2026-07-27
---

# Theologians Index — live queries

Auto-generated from the frontmatter of every note in `50 People/`. Nothing here is maintained by hand: add a person note with `era`, `region`, `school` and it appears below.

> [!info] The schema
> `type: person` · `dates:` · `tradition:` (prose) · **`era:`** biblical · patristic · medieval · classical-indian · reformation · nineteenth-century · indian-renaissance · since-1918 · **`region:`** · **`school:`** · **`ford_type:`** 1–5, **present only where Ford explicitly names the type** (Barth, Bonhoeffer, de Lubac, Balthasar = 2; Tillich = 3; Bultmann, Pannenberg = 4). Everything else is deliberately left blank rather than guessed — see [[01 - What Makes Theology Modern - Ford's Map]].

## Everyone, by era

```dataview
TABLE dates AS "Dates", region AS "Region", school AS "School"
FROM "50 People"
WHERE era
SORT era ASC, dates ASC
GROUP BY era
```

## The modern field (since 1918), by region

```dataview
TABLE dates AS "Dates", school AS "School"
FROM "50 People"
WHERE era = "since-1918"
SORT region ASC, dates ASC
GROUP BY region
```

## By school

```dataview
TABLE rows.file.link AS "Theologians"
FROM "50 People"
WHERE school
GROUP BY school
SORT school ASC
```

## Ford's five types — where the book states them

```dataview
TABLE dates AS "Dates", region AS "Region", school AS "School"
FROM "50 People"
WHERE ford_type
SORT ford_type ASC
GROUP BY "Type " + ford_type
```

## The Indian and Asian bench

```dataview
TABLE dates AS "Dates", school AS "School", region AS "Region"
FROM "50 People"
WHERE contains(region, "India") OR contains(region, "Asia")
SORT dates ASC
```

## Liberation, feminist, black, postcolonial

```dataview
TABLE dates AS "Dates", region AS "Region", school AS "School"
FROM "50 People"
WHERE contains(school, "liberation") OR contains(school, "feminist") OR contains(school, "womanist") OR contains(school, "black") OR contains(school, "postcolonial") OR contains(school, "minjung")
SORT dates ASC
```

## Orphans and gaps — maintenance

Person notes still missing the schema:

```dataview
LIST
FROM "50 People"
WHERE !era OR !region OR !school
```

Person notes nobody links to:

```dataview
LIST
FROM "50 People"
WHERE length(file.inlinks) = 0
```

## Related
[[Theology MOC]] · [[13 - Master Roster of Modern Theologians]] (the curated table, with significance and use today) · [[10 - Major Theologians and Their Methods]] (pre-1918) · [[Modern Theologians Since 1918 - Course Home]]
