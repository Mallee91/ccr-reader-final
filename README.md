# CC&R Reader

Browser-based HOA CC&R due-diligence reader.

## End-user experience

The finished app is intended to run as a normal HTTPS website. Users do not need VS Code, Python, Node.js, Live Server, or any local server.

1. Open the published website.
2. Enter their own Google AI Studio Gemini API key.
3. Upload a CC&R PDF.
4. The browser extracts selectable PDF text or performs OCR on scanned pages.
5. The browser sends extracted text directly to Google's Gemini API for analysis.

The PDF itself is processed in the user's browser and is not uploaded to this site's hosting service.

## Free deployment target

This project is designed for GitHub Pages. GitHub Pages can host static HTML/CSS/JavaScript sites on GitHub Free when the repository is public.

The repository should contain `index.html` at its top level.

## Important API-key model

This app intentionally asks each user for their own Gemini API key. Do not put a personal/shared Gemini API key into `index.html` or commit one to GitHub.

Google's current Gemini documentation recommends appropriate key restrictions and warns against exposing unrestricted keys publicly. Each user should use their own key and follow Google's current API-key guidance.

## Local development

Do not double-click `index.html` for development. That opens the page with a `file://` URL and can trigger browser origin/security restrictions.

For local development, use a local HTTP server such as VS Code Live Server. This is only for development; end users use the published HTTPS site.

## Files

- `index.html` — complete application
- `README.md` — deployment and handoff notes
- `.nojekyll` — prevents unnecessary Jekyll processing on GitHub Pages
