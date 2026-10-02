# Local HTTPS for phone clipboard access

The browser's Clipboard API requires a secure context. A phone opening a LAN IP over plain HTTP can send and receive text, but must copy it manually. A trusted HTTPS connection enables the Copy button, subject to browser permission. See [MDN](https://developer.mozilla.org/en-US/docs/Web/API/Clipboard/writeText).

## Optional Caddy example

1. Install [Caddy](https://caddyserver.com/docs/install) separately if desired.
2. Find your Windows computer's Wi-Fi IPv4 address with `ipconfig`. Replace `192.168.1.50` in `examples/Caddyfile` with it.
3. Keep ClipboardBridge listening on localhost and set the address that your phone will visit:

   ```powershell
   $env:HOST = '127.0.0.1'
   $env:PUBLIC_URL = 'https://192.168.1.50'
   npm start
   ```

4. In another terminal, from the project folder:

   ```sh
   caddy run --config examples/Caddyfile
   ```

5. Allow HTTPS port 443 through the private-network firewall if required. Visit `https://192.168.1.50` on both devices.
6. Install and trust **your own Caddy local root certificate** on each test device. Transfer the public root certificate, never the CA private key. Caddy attempts local computer trust; phones need their own trust setup. On iOS, a manually installed root certificate also needs full trust enabled in **Settings → General → About → Certificate Trust Settings**. Follow [Apple's certificate instructions](https://support.apple.com/en-ie/102390).
7. Confirm the browser reports a trusted connection and the page says copying is available. Create a new room and scan its HTTPS QR link. Test copying and pasting into another app.

Caddy's reverse proxy supports WebSocket upgrades, so the same route forwards `/signal` without a separate proxy rule. `tls internal` uses its local certificate authority; no public domain is needed. Details: [Caddy reverse_proxy](https://caddyserver.com/docs/caddyfile/directives/reverse_proxy), [local HTTPS](https://caddyserver.com/docs/automatic-https), [tls internal](https://caddyserver.com/docs/caddyfile/directives/tls).

This is a configuration example, not an installed or verified proxy on this computer. If you use a different proxy, forward `/signal` with WebSocket support and preserve the original Host header. Configure `PUBLIC_URL` as an origin without a path. Merely setting that environment variable does not create TLS or trust a certificate. After switching from HTTP to HTTPS, pair again because browser storage is scoped to the origin.
