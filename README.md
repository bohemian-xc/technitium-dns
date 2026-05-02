# technitium-dns

This repository contains a Docker Compose setup to run Technitium DNS inside a container attached
to macvlan networks so the container can participate on the LAN and receive broadcast traffic
(required for DHCP services).

Prerequisites
- A Docker host with macvlan support and two external macvlan networks created (for example
	an `app_net` for the web console and a separate `dhcp_net` for DHCP traffic).

Typical steps
1. Create macvlan networks on the Docker host (adjust names to match `.env`).
2. Copy `.env.example` to `.env` and set `APP_NET_NAME`, `DHCP_NET_NAME`, and IP addresses.
3. Run `docker compose up -d`.

Important notes
- The container must be attached to a macvlan network that allows it to receive broadcasts
	from the LAN for DHCP to work. On many systems you must configure the parent interface and
	gateway correctly when creating macvlan networks.
- Do not commit your `.env` (it is ignored by `.gitignore`). Use `.env.example` as a template.
- Ports in `compose.yml` are bound to the `APP_NET_IPADDR` address to keep traffic on the
	selected macvlan interface.

See `compose.yml` for the service configuration and `vol/` for persistent data.
