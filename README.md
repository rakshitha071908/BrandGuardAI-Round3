# BrandGuard AI — secure working build

BrandGuard AI reviews marketing copy with Gemini or OpenAI, stores decisions in a protected team workspace, and can create unpublished drafts in WordPress.

## Start on your computer

1. Install Node.js 18 or newer.
2. Open a terminal in this folder and run `node server.js` (opens on port 3100 if no PORT is set) (npm is not required).
3. Open `http://localhost:3100`.
4. First visit: create the owner account on this computer. Use a unique password with at least 12 characters.
5. Open **Team workspace → Connect integrations**. Choose Gemini free tier or OpenAI and paste that provider's API key; if available, add WordPress site URL, username and WordPress Application Password. Press **Save integration settings**. The app writes these secrets to the ignored `.env` file on this computer. The UI does not show a saved key again.
6. Add team members with separate reviewer/editor accounts. Share their temporary passwords privately.

For no-cost evaluation, choose Gemini in **Team workspace → Connect integrations**, paste a key from [Google AI Studio](https://aistudio.google.com/app/apikey), and save it. Gemini free-tier quotas and eligibility apply. OpenAI API requires available API credits.

Provider API keys stay on the server. Draft text submitted for review is sent to the selected AI provider. On the Gemini free tier, Google states content may be used to improve its products; review its current terms before sending sensitive drafts. The API returns a structured review and rewrite; a person still decides whether to approve it. AI output can be wrong.

## WordPress setup

Use a WordPress user that is allowed to create posts. In that user's profile, create an **Application Password**; then enter the HTTPS site URL, username and Application Password in the integration form. **Save WordPress draft** creates a post with `status: draft`. It does not publish. The button sends the original reviewed draft text, not the rewrite; apply the rewrite first if that is what you intend to save.

## Team login and roles

- Passwords are stored as salted scrypt hashes, not plain text.
- Sessions use random, HttpOnly, SameSite=Strict cookies and expire after eight hours; HTTPS deployments also set Secure.
- Login attempts are rate-limited in memory.
- The server enforces owner/reviewer/editor permissions. Only the owner can create accounts or clear decision history; owner and reviewer can record approvals and send WordPress drafts.
- First owner setup is restricted to localhost. For a new hosted deployment, set `ADMIN_EMAIL` and a unique `ADMIN_PASSWORD` (12+ characters) as private host environment variables before the first start. Never commit `.env`.

## Hosting

This server app needs a Node.js web service, not a static-only host. Configure the host's private environment variables: `NODE_ENV=production`, `ADMIN_EMAIL`, `ADMIN_PASSWORD`, ``AI_PROVIDER`, `GEMINI_API_KEY`, optional `GEMINI_MODEL`, `OPENAI_API_KEY`, optional `OPENAI_MODEL`, `WORDPRESS_URL`, `WORDPRESS_USERNAME`, and `WORDPRESS_APP_PASSWORD`. Set the start command to `node server.js` (opens on port 3100 if no PORT is set). In production, the app disables editing secrets through its own API; put them in the host's secret environment-variable settings.

## Honest limitations

- The LLM is decision support, not legal/compliance approval or factual evidence verification.
- WordPress integration creates drafts only; it does not publish or connect other CMS providers.
- Workspace records use a local JSON file and the server runs as one instance. Use a durable single-instance disk or migrate to a database before relying on persistent records; a free host may erase local-file changes on restart/redeploy.
- This is a hackathon implementation. For a production multi-customer service, add a managed database, CSRF token strategy, account recovery/MFA, audit retention, backups, monitoring and a formal security review.

## Health check

Open `/api/health`. It reports whether the server, AI key and CMS credentials are configured without exposing credential values.

