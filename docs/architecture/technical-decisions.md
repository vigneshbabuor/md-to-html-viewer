# Technical Decisions

## Decision 1: Pure Client-Side Static App vs Backend Rendering
- **Decision:** Pure client-side static web application with vanilla JS and CDN/vendored libraries.
- **Reason:** Instant latency, zero server hosting costs, offline capability, zero server-side attack surface.
- **Alternatives:** Node.js/Express server with SSR, Next.js SPA.
- **Consequences:** Limits storage to browser storage quota (~5MB). Client CPU handles parsing.

## Decision 2: Parsing & Sanitization Libraries
- **Decision:** Use `marked` for Markdown parsing and `DOMPurify` for HTML sanitization.
- **Reason:** `marked` is lightweight and fast. `DOMPurify` is gold standard for XSS prevention.
- **Alternatives:** `markdown-it`, `showdown`, custom regex sanitizers.
- **Consequences:** Need to ensure DOMPurify always wraps `marked.parse` output before DOM insertion.

## Decision 3: Export Mechanism via Blob and Native Print
- **Decision:** Use `Blob` + `URL.createObjectURL` for file downloads and `@media print` with `window.print()` for PDF/printing.
- **Reason:** Native browser APIs, zero external PDF libraries (e.g. `jspdf` or `html2pdf`) needed, minimal bundle size.
- **Alternatives:** Heavy JS PDF generation libraries.
- **Consequences:** PDF styling relies on browser print engine formatting.

## Decision 4: No Build Tooling / Vanilla Modules
- **Decision:** Native ES modules or simple script imports with vendor fallbacks.
- **Reason:** Minimal friction, instant local running, zero dependency drift or build pipeline overhead.
- **Alternatives:** Webpack, Vite, Parcel.
- **Consequences:** Manual vendor script updates.
