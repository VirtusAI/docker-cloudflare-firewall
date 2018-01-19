Firewall rules to whitelist [Cloudflare IP addresses](https://www.cloudflare.com/ips/) on ports 80 and 443 (based on [confd-firewall](https://hub.docker.com/r/colinmollenhour/confd-firewall/)).

[![](https://images.microbadger.com/badges/image/virtusai/docker-cloudflare-firewall.svg)](https://microbadger.com/images/virtusai/docker-cloudflare-firewall "Get your own image badge on microbadger.com")

Background
----------

This image allows firewall rules to be managed by a docker container which blocks traffic to the public interface from non-whitelisted addresses. Iptable rules are added to the `mangle` table.

Environment Variables
---------------------

 - FW_DISABLE - If set to 1, disables the firewall (removes the firewall table rules)

Usage
-----

Run with:

```
$ docker run -d --name docker-cloudflare-firewall --restart=always --cap-add=NET_ADMIN --net=host virtusai/docker-cloudflare-firewall
```

Or with docker-compose.yml:

```
version: '2'
services:
  firewall:
    restart: always
    image: virtusai/docker-cloudflare-firewall
    container_name: docker-cloudflare-firewall
    cap_add:
      - NET_ADMIN
    network_mode: host
```

List affected rules:

*Raw*

```
$ sudo iptables-save -t mangle
```

*Formatted*

```
$ sudo iptables -L -n -v -t mangle
```

To persist the firewall rules, just run the container with the `--restart=always` option.

Credits
-------

 - [confd-firewall](https://hub.docker.com/r/colinmollenhour/confd-firewall/) (by [colinmollenhour](https://github.com/colinmollenhour))

