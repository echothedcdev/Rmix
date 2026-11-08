# RMIX

RMIX is a separate project from Ecion. It connects a streamer's Nightbot song-request queue to a Lightstream browser-source player.

## Status

- [x] RMIX Supabase project created in US East (Ohio)
- [x] Secure database foundation and Row Level Security
- [x] Nightbot OAuth start/callback functions deployed
- [x] Nightbot live queue reader deployed
- [x] RMIX account and queue UI added to the website
- [ ] Nightbot OAuth app secrets configured by project owner
- [ ] Complete end-to-end Nightbot authorization test
- [ ] Lightstream player and audio playback
- [ ] Browser-source test in a real Lightstream broadcast

## Links

- Website: https://echothedcdev.github.io/Rmix/
- Repository: https://github.com/echothedcdev/Rmix
- Setup instructions: [SETUP.md](./SETUP.md)

## Security

Nightbot access and refresh tokens are encrypted server-side. Private connection data is not readable from the public browser client. Never commit client secrets, encryption keys, Supabase secret keys, or service-role keys to this repository.

## Music rights

Only stream audio you have permission to broadcast. RMIX does not bypass platform restrictions or copyright rules.
