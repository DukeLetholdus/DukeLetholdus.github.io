---
title: OpenVPN docker user management
date: 2023-01-13 17:30:00 +/-TTTT
categories: [Homelab, Software]
tags: [homelab, software, website, webserver]     # TAG names should always be lowercase
---
# How to manage user certificates in OpenVPN docker

* Initial certificate generation

```bash
docker compose -f openvpn.yml run --rm openvpn ovpn_genconfig -u udp://VPN.SERVERNAME.COM
docker compose -f openvpn.yml run --rm openvpn ovpn_initpki
```

* Start OpenVPN docker container

```bash
docker compose -f openvpn.yml up -d
```

* You can access the container logs with

```bash
docker compose -f openvpn.yml logs -f
```

* Generate a client certificate

```bash
export CLIENTNAME="your_client_name"
# with a passphrase (recommended)
docker compose -f openvpn.yml run --rm openvpn easyrsa build-client-full $CLIENTNAME
# without a passphrase (not recommended)
docker compose -f openvpn.yml run --rm openvpn easyrsa build-client-full $CLIENTNAME nopass
```

* Retrieve the client configuration with embedded certificates

```bash
docker compose -f openvpn.yml run --rm openvpn ovpn_getclient $CLIENTNAME > $CLIENTNAME.ovpn
```

* Revoke a client certificate

```bash
# Keep the corresponding crt, key and req files.
docker compose -f openvpn.yml run --rm openvpn ovpn_revokeclient $CLIENTNAME
# Remove the corresponding crt, key and req files.
docker compose -f openvpn.yml run --rm openvpn ovpn_revokeclient $CLIENTNAME remove
```
