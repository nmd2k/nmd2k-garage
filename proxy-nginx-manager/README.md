# Proxy-nginx-manager

To install, run docker compose. The proxy manager will apear on port 81.

## Generate SSL cert
Go to tab "SSL Certificates", add your desire domain name (e.g. `*.nmd2k.io.vn` for all subdomain of nmd2k.io.vn).

Check "Use a DNS Challenge" and select Cloudflare as your DNS provider. Now you might need to generate a Cloudflare API key that access to the corresponding DNS. Run and check logs if fail.
