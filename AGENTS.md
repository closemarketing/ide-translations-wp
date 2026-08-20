# Translation Project — WordPress Plugins & Sites

This repository contains translation files for WordPress plugins and sites (Close·technology, close.marketing, etc.).

## Project structure

```
glossary/               WordPress core glossary CSVs per locale
  locale-es.csv         Spanish glossary
  locale-fr.csv         French glossary
  locale-it.csv         Italian glossary
  locale-de.csv         German glossary

translations-xliff/     XLIFF files from WPML translation jobs
  <job-folder>/         One folder per translation job (any site/language pair)

wp-plugins-*.po         PO files for WordPress.org plugin translations
```

## File types

### XLIFF (`.xliff`)
Exported from WPML. Structure: `<source>` (original) → `<target>` (translation).  
- `state="translated"` — done  
- `state="needs-review-translation"` — auto-suggestion, needs human review  
- No `state` attribute — untranslated (source text copied to target)

### PO (`.po`)
Standard gettext format for WordPress.org plugin translations.  
- `msgid` = English source  
- `msgstr` = translation  
- Empty `msgstr ""` = untranslated

## Translation rules (all languages)

- Always use informal register ("tú", "tu", "tu", "du" — never formal).
- Do **not** translate plugin or theme names. E.g. "Contact Form 7" stays as-is.
- Brand names that must never be translated: `Close·technology`, `Close·tech`, `Close·marketing`, `FormsCRM`, `Odoo`, `Factusol`, `Holded`, `Clientify`, `FacturaDirecta`, `Datisa`, `WooCommerce`, `WordPress`.
- Translate contextually, not literally. "Page Management Documentation" → "Documentación de la gestión de páginas", not "Documentación gestión páginas".
- URLs, file paths, `msgctxt` values, and HTML class/ID attributes must not be translated.
- Preserve all HTML tags exactly — do not add, remove, or reorder attributes.

## Spanish (es)

- Use **comillas españolas** («»), never "straight quotes" or "curly quotes".
- No mid-sentence capitalisation except proper nouns and RAE-accepted exceptions.
- Do not translate font names (e.g. "System Fonts" → "Fuentes del sistema" is OK because it is a setting label, not a proper name).
- All "blog" references should use "sitio" (site) unless referring to an actual blogging platform (e.g. "Importar un blog de Blogger").
- Reference: `glossary/locale-es.csv` for all term decisions.

## French (fr)

- Reference: `glossary/locale-fr.csv`.

## Italian (it)

- Reference: `glossary/locale-it.csv`.

## German (de)

- Reference: `glossary/locale-de.csv`.

## English targets (XLIFF ES→EN)

- Used for translation sites (Spanish source → English target).
- Use natural, professional English — avoid literal translations.
- Titles use sentence case (only first word and proper nouns capitalised), unless the source uses full caps for stylistic headings.
- `state="translated"` for completed units; `state="needs-review-translation"` for auto-suggestions pending review.

## Common issues to watch for

- **Untranslated units**: target identical to source — must be translated.
- **Wrong product in target**: auto-suggestions sometimes pull content from another plugin page. Always verify the target matches the source's product/topic.
- **Spurious HTML tags**: `<br>` or `data-mce-bogus` tags added by TinyMCE — remove them.
- **Added attributes**: `target="_blank"` or `rel="noopener"` sometimes injected by the translation tool — only keep if present in source.
- **Lorem ipsum**: placeholder text left in targets — translate or flag.
