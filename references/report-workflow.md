# Management report workflow

Read this reference when creating or updating PPTX/XLSX deliverables.

## Presentation narrative

Use the existing deck as the visual source. A useful sequence is:

1. parsing dates and statistics periods;
2. total discovery change;
3. current competitive context for the requested geography;
4. stores with growth reserve;
5. stores that lost leadership;
6. stores that gained leadership;
7. gained-leadership stores with positive discovery growth;
8. parsing or profile errors;
9. implications and next actions.

Adjust the sequence to the user's request; do not add every section automatically.

## Leadership-loss table

Use these columns when available:

1. `Адрес магазина`;
2. `Текущее место` — use `2-е или ниже` when exact rank is unavailable;
3. `Кто занял 1-е место`;
4. `Возможная причина`;
5. `Яндекс Карты`.

If the table is too long, split it across consecutive slides rather than making body text unreadable.

## Positive-growth table

For stores that gained local leadership and also grew own discovery, show:

- address;
- absolute discovery increase, preferably with `было → стало`;
- percentage increase.

Show the aggregate `было → стало`, absolute increase, and percentage increase in the subtitle or callout.

## Language rules

- Use `магазины` for Petshop.ru locations.
- Use `локальные зоны` or `локальные сравнения` for repeated competitor leadership observations.
- Avoid `физические магазины конкурента` unless deduplicated competitor cards support the claim.
- Avoid `порог лидера`; use `трафик компании на 1-м месте`.
- Avoid causal certainty. Use `возможная причина`, `вероятно`, or a direct metric statement.

## Source notes

Every analytical slide should include a `[Sources]` block in speaker notes containing:

- source workbook and sheet/range;
- periods compared;
- geography filter;
- calculation definition;
- relevant limitation, such as unavailable exact rank or leader-card identity.

## Quality checks

Before delivery:

- reconcile headline leadership counts to transitions and unmatched rows;
- confirm every listed store appears in both intended periods unless explicitly labeled unmatched;
- verify percentage calculations from displayed counts;
- verify geography labels against `Регион`;
- ensure competitor counts are labeled as local comparisons, not stores;
- render every changed slide and inspect links, wrapping, clipping, and footers;
- preserve the template's masters, layouts, typography, and page numbering.
