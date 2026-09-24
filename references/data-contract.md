# Data contract and calculations

Read this reference whenever analyzing a Yandex Business competitor XLSX.

## Expected columns

The `Конкуренты` sheet normally contains:

- `Дата запуска`: when browser automation collected the row;
- `Пермалинк`: stable identifier for the analyzed Petshop.ru card;
- `Название`, `Адрес`, `Регион`, `Локация`, `URL`;
- `Период`: the statistics period displayed by Yandex Business;
- `Радиус, км`;
- `Запросов по категориям`, `Похожих компаний рядом`;
- `Переходов в похожие компании`;
- `Лидер`;
- `Переходов у лидера`;
- `Переходов в вашу компанию`;
- `Доля вашей компании`;
- `Доля от лидера`.

Confirm actual headers before calculating. Stop and explain missing required fields rather than silently substituting a different metric.

## Period selection

- Group rows by `Период`.
- Use `Дата запуска` only to label the parsing run.
- When more than two periods exist, compare the periods requested by the user; otherwise compare the two latest complete periods.
- Check row counts and duplicate permalinks within each period.

## Matching

Normalize `Пермалинк` as text and match on exact value.

Partition rows into:

- matched in both periods;
- present only in the earlier period;
- present only in the later period.

Do not drop unmatched rows from the reconciliation.

## Core metrics

For each period:

```text
total discovery = sum(Переходов в вашу компанию)
leader count = count(Лидер = "Petshop.ru")
```

For each matched store:

```text
discovery delta = current own discovery − previous own discovery
discovery growth % = discovery delta / previous own discovery
```

If previous discovery is zero, show the absolute change and mark percentage growth as unavailable instead of dividing by zero.

Leadership transitions:

```text
loss: previous leader = Petshop.ru AND current leader != Petshop.ru
gain: previous leader != Petshop.ru AND current leader = Petshop.ru
```

Positive-growth gains are gains with `discovery delta > 0`. Keep gains with flat or negative own discovery in the audit, but exclude them from a slide specifically labeled as growth.

## Geography

Trim whitespace before comparing `Регион`.

- Strict Saint Petersburg: `Регион = Санкт-Петербург`.
- Leningrad Oblast: `Регион = Ленинградская область`.
- Agglomeration: combine the two only when explicitly requested and label it `СПб + Ленинградская область`.

## Competitor leader counts

Counting `Лидер` values answers:

> In how many analyzed Petshop.ru local comparisons was this brand the leader?

It does not answer:

> How many physical stores does this competitor operate?

To count physical competitor stores, collect and deduplicate the leader card's organization ID or exact address in future parsing runs.

## Cause labels

Use concise evidence-backed labels:

- `Наш трафик 134 → 104 (−22%)`;
- `Доля от лидера 100% → 91%`;
- `Трафик компании на 1-м месте 427 → 469 (+42)`;
- `Наш трафик вырос, но остался ниже трафика нового лидера`.

Label these as possible explanations. Different periods may have different leader companies, radii, or competitive sets.

