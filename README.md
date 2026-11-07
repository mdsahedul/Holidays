# Public Holidays JSON Data (`holidays/`)

Lightweight, versioned JSON files for dynamic public holiday updates and date adjustments.

---

## 📁 Folder Structure

```text
holidays/
├── README.md        # Format reference & examples
├── version.json     # Per-country version numbers
└── BD.json          # Holiday list for Bangladesh (ISO code: BD)
```
*(Add `<ISO_CODE>.json` for any other country as needed, e.g., `SA.json`, `AE.json`, `MY.json`, `QA.json`.)*

---

## 📋 JSON Format & Examples

### 1. `version.json`
Increment the country's version number whenever its `<COUNTRY_CODE>.json` file is updated:
```json
{
  "BD": 1
}
```

### 2. `<COUNTRY_CODE>.json` (e.g. `BD.json`)
Clean default structure when no extra overrides are active:
```json
{
  "country": "BD",
  "version": 1,
  "updated": "2026-11-07",
  "holidays": []
}
```

### 3. Supported Actions Inside `"holidays": [ ... ]`

```json
{
  "country": "BD",
  "version": 2,
  "updated": "2026-12-01",
  "holidays": [
    {
      "_comment": "Example 1: Add a single-day holiday (e.g. Election Day or special holiday)",
      "date": "2026-12-28",
      "action": "ADD",
      "title": "জাতীয় সংসদ নির্বাচন উপলক্ষ্যে সাধারণ ছুটি",
      "category": "সরকারি ছুটি"
    },
    {
      "_comment": "Example 2: Add a multi-day range holiday (inclusive start..end)",
      "date": "2027-03-11..2027-03-12",
      "action": "ADD",
      "title": "ঈদুল ফিতর (নির্বাহী আদেশে অতিরিক্ত ছুটি)",
      "category": "সরকারি ছুটি (নির্বাহী আদেশ)"
    },
    {
      "_comment": "Example 3: Remove/cancel a default holiday on a specific date",
      "date": "2027-05-16",
      "action": "REMOVE"
    },
    {
      "_comment": "Example 4: Replace existing holiday(s) on a specific date with a new title",
      "date": "2027-05-17",
      "action": "REPLACE",
      "title": "পবিত্র ঈদুল আযহা (চাঁদ দেখা সাপেক্ষে পরিবর্তিত)",
      "category": "সরকারি ছুটি"
    }
  ]
}
```

---

## 🔄 Update Workflow

1. Edit `BD.json` (or `<COUNTRY_CODE>.json`) and add/modify/remove items inside `"holidays": [ ... ]`.
2. Increment the version number for that country in `version.json` (e.g. `"BD": 2`).
3. Commit and push the changes.
