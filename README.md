# Ad Coding Tool

A browser tool for multiple researchers to code ads and compare their results.

This repo holds **only the tool**. The study's private files are shared directly between researchers and are never committed:

| Private file | What it holds |
|---|---|
| `study_config.json` | Coding dimensions, the video check and the locked pilot set |
| `ads.csv` | The ad list |
| `ad-codes_*.csv` | Each coder's exported results |

## Pages

- **`index.html`** (coding): on first visit, choose the settings file and the ad list. Both are remembered in that browser.
- **`compare.html`**: upload two coders' exported results. The settings load automatically if you've used the coding page in the same browser.
- **`ads-manager.html`** (Add Ads to Dataset): add or fix ads and download an updated `ads.csv`. New ads get the next ID for their company automatically (e.g. `ANT-008`), and IDs can never be changed or reused.

## Updating settings or the ad list

1. Edit `study_config.json`, or use the ad list page.
2. If you changed the settings, raise `"version"` by 1.
3. Send the new file to the other coder. They open **Backup / Restore --> Load new settings or ad list** and pick it.

`study_config.json` is strict JSON. Keep these settings rules in mind when editing it:

- Add dimensions freely, but never rename an existing dimension's `"key"` or option text; saved codes use them.
- Each dimension has a `"key"` (the export column, with no spaces), `"label"`, `"help"`, and `"options"`. The optional `"ordinal"` lists ordered options from low to high for weighted kappa.
- `"video_check"` is the optional check shown on every ad to confirm the linked video is the actual ad.
- The `"pilot"` `"ids"` list is locked, so adding ads never changes it. To draw a new pilot, set `"ids"` to `[]`, change `"seed"`, load the file, then use **Backup / Restore → Copy pilot list** and paste the result back into `"ids"`.
- When `"ids"` is empty, ads are drawn from each company in proportion (each company gets at least one). Ads with any concern tag are skipped when `"excludeFlagged"` is `true`.

All content in this repository is copyrighted by David Alexander Hines (2026).

Exports record the settings version, and the compare page warns you if the two coders used different versions.

## Rules that protect existing codes

- Never rename a dimension's `key` or its option text. Add new dimensions instead.
- Never change or reuse an `ad_id`.
- The pilot set is the `"ids"` list under `"pilot"` in the settings file, so adding ads never changes it.
