# Web Phone Login

A single static page that collects an extension + password and hands off to the
WebVoIPPhone softphone.

## Files

| File | Purpose |
| --- | --- |
| `index.html` | The entire app — markup, CSS and JS in one file |
| `render.yaml` | Render Blueprint, so deploy is one click |
| `README.md` | This file |

## Configuration

Both settings live in the `CONFIG` block at the top of the `<script>` in
`index.html`:

```js
const CONFIG = {
  serverAddress: '139.84.175.21:65236',
  baseUrl: 'https://www.webvoipphone.com/webphone_online_demo/softphone.html'
};
```

Change them, commit, and Render redeploys automatically.

## Deploy on Render

**Option A — Blueprint (uses `render.yaml`)**

1. Go to <https://dashboard.render.com/blueprints>
2. **New Blueprint Instance** → pick this repo → **Apply**
3. Site comes up at `https://webphone-login.onrender.com`

**Option B — Manual static site**

1. <https://dashboard.render.com> → **New** → **Static Site**
2. Connect this repo
3. Build Command: *(leave empty)*
4. Publish Directory: `.`
5. **Create Static Site**

No build step, no environment variables, no server needed.

## Security notes

- The password is passed to `webvoipphone.com` in the URL query string. It will
  appear in browser history, proxy/server logs, and the `Referer` header. This is
  forced by the third-party demo page and cannot be fixed from this file alone.
- The SIP server address is hardcoded in the page and is visible to anyone who
  loads it. Treat it as public information.
- This is a shared public demo softphone at `webvoipphone.com`, not a private
  instance. Do not use it for credentials you would not want logged elsewhere.
- Because the site is public, anyone who finds the URL can load the dialer and
  attempt to authenticate against the PBX. Consider restricting access at the
  PBX (IP allow-list, fail2ban) or putting the page behind Render's basic auth /
  a Cloudflare Access policy.
