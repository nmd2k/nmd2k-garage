# WireGuard

To easily install WireGuard and using a GUI dashboard, try this https://github.com/wg-easy/wg-easy

Install via docker compose [docker-compose.yml](./docker-compose.yml)

## Notes:

* Accessing UI: Dashboard requires user using HTTPS request -> Recommend using proxy manager
* Adguard Home: Adguard Home routes internet though a device (e.g. 192.168.1.222), turn on wire guard will use the direct internet from router -> Fix: Add device LAN IP to DNS config (at admin panel)
* Port forwarding: In order to allow internet to wireguard, wireguard's port need to be forwarded (on the router, default to "51820")
