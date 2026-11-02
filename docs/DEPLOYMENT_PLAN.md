# FORGEPILOT deployment plan

## Service boundaries

1. `forgepilot-ai`: HTTPS-only public web app and Shopify OAuth callback, with durable database and backups.
2. `aura-intelligence`: private inference adapter, isolated from the public internet.
3. GPU model service: separately provisioned approved open-weight model running vLLM.
4. Background task workers: event-driven tasks with retries, idempotency, and audit records.

## Shopify

Register a Shopify app and configure exact HTTPS redirect URLs, requested scopes, signed OAuth state validation, token storage, and mandatory data privacy/uninstall webhooks. Test against a dedicated development store. Publishing/spending must require authorization.

## Production blockers

- Properly provisioned GPU inference, model licensing, resource sizing
- A production-grade durable database and backups
- Secret management, least-privilege networking, external security audit
- Customer authentication, email verification, recovery and billing
- Shopify partner/developer app configuration and live OAuth end-to-end tests
- Monitoring, incident response, privacy policy, terms, data export and deletion

Do not open public customer registrations until these gates pass.
