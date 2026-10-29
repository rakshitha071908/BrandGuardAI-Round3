# Test report — secure working build

## Passed on the local working copy
- `node --check server.js`
- `node --check app.js`
- Server starts on Node.js 24 with no npm dependencies.
- Health endpoint returns online/configuration status.
- Homepage includes owner setup/sign-in UI.
- Unauthenticated review API access returns 401.
- `.env`, server source, and data files are not web-served (404).
- First owner setup works from localhost; sign-in returns an authenticated session.
- Owner can create a team account.
- Editor is denied approval and integration-secret changes (403).
- Missing OpenAI key is reported as a clear configuration error (503).

## Needs real account configuration for live integration tests
- OpenAI review request and returned JSON/rewrite need the owner's valid API key.
- WordPress draft creation needs a real HTTPS WordPress site and Application Password.
- Browser click-through on the local updated copy is still needed after signing in.
- Hosted HTTPS, production Secure cookie, environment settings, persistent storage and redeploy behavior are not verified.

No real API key, CMS credential, or customer draft was used during checks.
