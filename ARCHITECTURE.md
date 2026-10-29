# Architecture — secure working build

Browser (HTML/CSS/vanilla JavaScript)
  → same-origin Node.js HTTP server (`server.js`)
      → Gemini generateContent API or OpenAI Chat Completions API (server-side key; structured JSON review)
      → WordPress REST API (server-side Application Password; creates `draft` posts only)
      → protected JSON data file (`data/workspace.json`)

All workspace APIs require a signed-in session except health, initial local setup, and login. Passwords are salted scrypt hashes. Sessions are random HttpOnly/SameSite cookies with an eight-hour lifetime and Secure cookies in production. Owner, reviewer and editor roles are checked on the server. Static serving is allowlisted so `.env`, server code and stored workspace records are not web-readable.

This is a single-server demo. Login and permissions are implemented, but this is not a production-ready multi-tenant SaaS: sessions are in memory, records are in a local JSON file, and recovery/MFA/database backups are not implemented.
