# System Architecture: Markdown to HTML Converter

## Architecture Overview
Pure client-side static web application. No backend server, no database.

- **Parser Layer**: `marked.js` parsing Markdown to HTML AST/string.
- **Sanitizer Layer**: `DOMPurify` enforcing strict XSS prevention rules.
- **UI Engine**: Vanilla JS + CSS Grid/Flexbox split view.
- **Export System**: Browser native `Blob` download + `window.print()` CSS print profile.
- **Storage Layer**: Native `window.localStorage` with quota protection.

## Security Architecture
Strict DOMPurify sanitization rules configured for tags, attributes, and URI schemes. No inline execution vulnerabilities allowed.
