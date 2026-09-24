---
name: yandex-business-competitor-report
description: Analyze repeated XLSX parsings from the Yandex Business «Конкуренты» section, reconcile discovery traffic and local leadership by store, and update management PPTX/XLSX reports. Use when comparing parsing periods, identifying stores that gained or lost leadership, analyzing competitors by geography, or extending the established Petshop.ru competitor presentation. Do not use to count competitors' physical stores unless their card IDs or addresses were collected.
---

# Yandex Business Competitor Report

Build an auditable comparison of Yandex Business competitor parsings and turn it into a concise Russian-language management report.

For standalone workbook analysis or authoring, also follow the `spreadsheets:Spreadsheets` skill. For PowerPoint work, also follow the `presentations:Presentations` skill and preserve the supplied deck's design.

## Inputs

Prefer:

- an XLSX containing at least two parsing periods on a `Конкуренты` sheet;
- an existing PPTX when the user wants slides added or updated;
- an optional error sheet or error workbook.

If multiple parsing runs are stored in one file, treat them as separate snapshots. Do not infer periods from the filename alone.

## Required workflow

1. Inspect the workbook before editing or reporting.
2. Read [references/data-contract.md](references/data-contract.md) before calculating metrics.
3. Identify the two comparison periods from `Период` and retain `Дата запуска` as collection metadata.
4. Match stores by normalized `Пермалинк`. Never use address text as the primary key.
5. Reconcile matched, missing, and newly appearing stores before stating leadership gains or losses.
6. Calculate totals and transition lists from row-level data, not by subtracting headline counts.
7. If producing slides, read [references/report-workflow.md](references/report-workflow.md) and update the supplied template through inherited or duplicated template slides.
8. Verify all headline counts against the row-level transition tables.

## Non-negotiable interpretation rules

- Call Petshop.ru locations `магазины`, not `филиалы`, unless the user explicitly requests otherwise.
- A competitor name in `Лидер` identifies the leader of a local comparison around a Petshop.ru store. Repeated appearances are `локальные зоны` or `локальные сравнения`, not physical competitor stores.
- Do not claim a competitor has N stores unless unique competitor card IDs or addresses are present and deduplicated.
- `Лидер = Petshop.ru` does not prove that the analyzed Petshop.ru card itself has the leader traffic value; another nearby Petshop.ru card may be the local leader.
- The export does not contain Petshop.ru's exact rank after losing leadership. Report `2-е или ниже`, and disclose the limitation.
- Use the exact `Регион` field for strict geography. `Санкт-Петербург` excludes `Ленинградская область`; combine them only when the user requests the agglomeration.
- Treat possible causes as hypotheses. Prefer evidence such as `наш трафик −N`, `доля от лидера X% → Y%`, or `трафик компании на 1-м месте A → B`. Never use the ambiguous phrase `порог лидера`.
- Do not describe movement as `перераспределение позиций` unless the data contains actual ranks. Say that a brand became leader in more or fewer local comparisons.
- Do not include median share in management slides unless the user asks for it.

## Reconciliation gate

Before delivery, prove the leadership count with:

```text
current leaders
= previous leaders
− matched stores that lost leadership
+ matched stores that gained leadership
− previous leader stores missing from the current parsing
+ new current stores that are leaders
```

Report gross losses and gross gains separately. A net change alone cannot determine either value.

## Output expectations

For management reporting, prioritize:

- total own discovery by period and absolute/percentage change;
- leader counts by explicit geography;
- all stores that lost leadership;
- all stores that gained leadership;
- the subset of gained-leadership stores with positive own-discovery growth;
- processing errors and unmatched stores;
- concrete follow-up actions.

Keep source ranges and methodology in speaker notes or workbook source fields. Preserve clickable Yandex Maps links when the permalink supports them.
