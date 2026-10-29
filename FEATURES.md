# Features — secure working build

- Gemini and OpenAI copy review and rewrite via server-side API calls; Gemini free-tier option for evaluation.
- Findings normalized and validated before display; human approval remains required.
- One-time local owner setup, sign in/sign out, scrypt password hashes and expiring HttpOnly session cookies.
- Server-enforced owner/reviewer/editor permissions and owner-created team accounts.
- Gemini, OpenAI and WordPress secrets configured from the owner screen and kept out of source code; hosted mode requires host-managed secrets.
- WordPress REST integration creates an unpublished draft only.
- Protected review history, decisions, assignments and comments.
- Static file allowlist; private data and environment files are not web-served.

## Needs the owner's accounts
Real AI analysis needs a Gemini or OpenAI API key. Gemini free-tier quotas and availability apply; OpenAI requires API credits. Live WordPress draft creation needs the WordPress site's HTTPS URL and an Application Password. These are not included in the source bundle.
