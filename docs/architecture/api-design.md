# API Design: Markdown to HTML Converter

## Pure Client-Side Internal Modules API

### 1. Parser Engine (`js/parser.js`)
- `initParser(options)`: Configures marked and DOMPurify hooks.
- `renderMarkdown(markdownString): string`: Parses and sanitizes markdown to secure HTML string.

### 2. State Store (`js/state.js`)
- `getState(): AppState`: Returns active application state snapshot.
- `setState(partialState)`: Merges state and notifies subscribers.
- `subscribe(listener)`: Subscribes UI components to state changes.

### 3. Exporter (`js/exporter.js`)
- `downloadHtml(htmlString, title)`: Creates HTML `Blob` and triggers file download.
- `downloadMarkdown(markdownString, title)`: Creates `.md` `Blob` and triggers file download.
- `copyToClipboard(text): Promise<boolean>`: Copies string to user clipboard via `navigator.clipboard`.
- `triggerPrint()`: Invokes native `window.print()`.

### 4. Storage Adapter (`js/storage.js`)
- `loadDraft(): string|null`: Fetches draft from `localStorage`.
- `saveDraft(content: string): boolean`: Saves draft to `localStorage` with quota exception guard.
- `loadPreferences(): object`: Loads theme and layout preferences.
- `savePreferences(prefs: object)`: Saves preferences to `localStorage`.
