# Database Design: Markdown to HTML Converter

## Database Architecture
Zero backend database required. Pure client-side static application.

## Client-Side Storage Schema (Web Storage API)
Keys stored in `window.localStorage`:

1. `md2html:content`
   - Type: `string`
   - Purpose: Current autosaved Markdown document buffer.
2. `md2html:settings`
   - Type: `JSON string`
   - Schema:
     ```json
     {
       "theme": "light" | "dark" | "system",
       "layout": "split" | "editor" | "preview",
       "syncScroll": true,
       "autoSave": true
     }
     ```

## Quota & Fallback Strategy
- Try/catch around all `localStorage.setItem` calls.
- In case of `QuotaExceededError`, disable persistence, display notification in Status Bar, maintain state in browser memory.
