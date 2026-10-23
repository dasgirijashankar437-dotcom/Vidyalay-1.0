# Vidyalay 1.0 — Powered by NOVYRA VYREN

Royal navy-and-gold landing-page prototype for Vidyalay 1.0.

## Current scope
- Landing screen and responsive royal theme
- Sign-in, login, WhatsApp, and Telegram modal flows (preview only)
- Client-side password-strength checks for the preview
- Dashboard intentionally out of scope until requested

## Important: authentication is not live yet
The current page is a front-end prototype. It does **not** send email verification links, create accounts, authenticate logins, or send WhatsApp/Telegram messages. Do not enter real passwords in this preview.

A production release needs:
1. An authentication/backend provider (for email verification, secure password handling, sessions, and account storage).
2. Redirect/callback URLs configured for the deployed site.
3. A WhatsApp Business Platform provider and approved messaging setup if WhatsApp community invitations/links are required.
4. A Telegram bot and the intended public/private community link; bots cannot silently confirm every kind of user membership without suitable bot permissions and implementation.
5. Environment secrets configured in the provider/deployment settings, never committed into this repository.

## Preview / deploy
The site entry point is `index.html`. GitHub Pages can serve this static preview. This alone does not provide a backend or make the auth flows real.

## Manual smoke-test checklist
- [ ] Landing page loads at desktop width
- [ ] Landing page adapts to mobile width
- [ ] Sign in opens email field
- [ ] Email form advances to User ID/password preview and clearly warns no email was sent
- [ ] Login opens User ID/password and clearly warns backend is not connected
- [ ] WhatsApp and Telegram buttons open the relevant contact form and do not claim a message was sent
- [ ] Weak passwords are rejected by preview validation
- [ ] Dialog closes with close button, outside click, and Escape
- [ ] Verify old `vidyalay-royal-ui` repository remains untouched

Do not mark these as passed until tested in a browser.