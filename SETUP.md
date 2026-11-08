# RMIX setup

RMIX is separate from Ecion. Its Supabase project is:
- Project ref: `auyaicguvjjkipdcppgm`
- Region: US East (Ohio), `us-east-2`
- Project URL: `https://auyaicguvjjkipdcppgm.supabase.co`

## What is already deployed

- Database tables for RMIX settings, encrypted Nightbot credentials, one-time OAuth state, player sessions, and queue cache.
- Row Level Security on every RMIX table.
- Direct browser access to Nightbot tokens and private backend tables is blocked.
- Edge Functions: `nightbot-connect`, `nightbot-callback`, and `nightbot-queue`.
- GitHub Pages frontend with RMIX sign-in/sign-up and live Nightbot queue UI.

## One-time setup you must do

### 1. Enable the GitHub Pages URL in Supabase Auth

In Supabase Dashboard → Authentication → URL Configuration:
- Site URL: `https://echothedcdev.github.io/Rmix/`
- Add that same URL to Redirect URLs.

### 2. Register the Nightbot OAuth application

In Nightbot's account applications area, create an OAuth application:
- Application name: `RMIX`
- Redirect URL (copy exactly): `https://auyaicguvjjkipdcppgm.supabase.co/functions/v1/nightbot-callback`
- Required scope: `song_requests_queue`

Keep the Nightbot client secret private. Do not put it in GitHub or send it in chat.

### 3. Add Edge Function secrets

In Supabase Dashboard → Project Settings / Edge Functions → Secrets (the Functions Secrets page), add:

| Secret name | Value |
| --- | --- |
| `NIGHTBOT_CLIENT_ID` | Client ID from the Nightbot OAuth app |
| `NIGHTBOT_CLIENT_SECRET` | Client secret from the Nightbot OAuth app |
| `NIGHTBOT_REDIRECT_URI` | `https://auyaicguvjjkipdcppgm.supabase.co/functions/v1/nightbot-callback` |
| `RMIX_TOKEN_ENCRYPTION_KEY` | A fresh base64-encoded 32-byte random key |

Generate the encryption key locally in Windows PowerShell (do not post it anywhere):
```powershell
$bytes = New-Object byte[] 32
[Security.Cryptography.RandomNumberGenerator]::Create().GetBytes($bytes)
[Convert]::ToBase64String($bytes)
```

Paste the generated output only into the `RMIX_TOKEN_ENCRYPTION_KEY` secret field. Keep a secure backup. If this key is lost or changed, saved Nightbot tokens cannot be decrypted and Nightbot must be reconnected.

### 4. Publish the website

In GitHub → `echothedcdev/Rmix` → Settings → Pages:
- Deploy from a branch
- Branch: `main`
- Folder: `/ (root)`

Website: `https://echothedcdev.github.io/Rmix/`

### 5. Test

1. Open the website.
2. Create an RMIX account and confirm the email if Supabase asks.
3. Sign in.
4. Press **Connect** beside Nightbot and approve the requested queue permission.
5. Press **Refresh** under Nightbot live queue.

## Current limitations

The live Nightbot queue reader is deployed. The Lightstream browser-source player and actual audio playback are not finished yet. Do not expect the demo controls to stream audio. Lightstream supports HTTPS browser-source URLs, but the player still needs to be built and tested in a real Lightstream project.

Only play music you have permission to use in your stream. Never publish Supabase secret/service-role keys or Nightbot client secrets in the frontend or repository.
