# Vidyalay 1.0 — Supabase backend preparation

This folder is preparation only. It does not mean a hosted Supabase project exists or that production authentication/messaging is live.

## Create the hosted project
1. Sign in at https://database.new (official Supabase project creation shortcut).
2. Choose **New project**, select the organization, enter project name `Vidyalay 1.0`, set a strong database password, and choose a region close to your users.
3. Wait until the project is ready.
4. In the project dashboard, open **Connect** or **Project Settings → API Keys** and copy the Project URL and **publishable** key (starts with `sb_publishable_` in the current key format).
5. Keep database passwords, secret keys, `service_role` keys, WhatsApp tokens, and Telegram bot tokens private. Do not commit them or paste them into chat.

## Configure auth
1. In **Authentication → URL Configuration**, set the Site URL to the real deployed Vidyalay URL when available.
2. Add exact allowed Redirect URLs for local development and the deployed site. Do not leave the example GitHub Pages wildcard as a production assumption; replace it with the actual URL.
3. In **Authentication → Sign In / Providers** (wording can vary), keep Email enabled and require email confirmation.
4. For production email delivery, configure a verified SMTP provider under the Auth email settings; the default service may have restrictive sending limits.
5. Use the confirmation email redirect to a dedicated callback/create-credentials page. This callback has not been implemented yet.

## Local environment
Copy `.env.example` to `.env.local` and fill in the actual URL and publishable key. Keep `.env.local` ignored by Git. The publishable key is suitable for browser clients only when database access is protected with Row Level Security.

## Apply schema later
After the project ref is known and the migration has been reviewed:
```sh
npx supabase@latest login
npx supabase@latest link --project-ref YOUR_PROJECT_REF
npx supabase@latest db push
``
Review the migration and redirect URLs before pushing. Do not run commands with placeholder values.

## Planned authentication implementation
- Email signup → verification email → callback → create User ID/password → sign-in.
- Login with the same account credentials.
- Do not store passwords in application tables; Supabase Auth must handle password storage.
- WhatsApp and Telegram onboarding require separate, server-side provider integrations. Do not claim messages are sent until credentials are configured and live delivery is tested.
- WhatsApp/Telegram provider tokens belong in **Edge Function Secrets**, never in Git or client JavaScript.

Official references:
- Create project: https://database.new
- Auth quickstart: https://supabase.com/docs/guides/auth
- API keys: https://supabase.com/docs/guides/getting-started/api-keys
- Redirect URLs: https://supabase.com/docs/guides/auth/redirect-urls
- Edge Function secrets: https://supabase.com/docs/guides/functions/secrets
