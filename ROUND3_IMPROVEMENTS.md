# Round 2 → updated build commitments

1. **Context-aware review grounded in guidance/evidence:** The review now calls the configured OpenAI API and returns findings and a rewrite. This is not a retrieval system for approved company policies and does not independently verify claims; reviewers must confirm evidence.
2. **Shared team workflow:** Workspace sign-in, scrypt password hashes, expiring secure cookies, and server-enforced owner/reviewer/editor roles are implemented. Owner creates accounts. Persistent records still use a single-instance JSON file; MFA, account recovery and managed database are future work.
3. **CMS pre-publication integration:** WordPress REST integration creates unpublished draft posts. It does not publish. Other CMS platforms are not implemented.

Live OpenAI review requires the team's API key. Live WordPress draft creation requires the team's site and Application Password. Never claim those live integrations were verified until tested with the team's own accounts.
