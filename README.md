Descr:
Wget IP ranges, and announce it via BGP for you router.

Install bird 1.6.8

1.1.1.1 - you VPS/server with bird service
8.8.8.8 - your bgp client (Mikrotik)

Mikrotik config
```
[admin@mikrotik] /routing/bgp> export
# 1989-08-14 15:50:00 by RouterOS 7.15.2
# software id = 3VLR-GKZ4
#
# model = C53UiG+5HPaxD2HPaxD
# serial number = XYZ
/routing bgp template
add as=65000 disabled=no name=geo-bgp.template output.network=bgp-networks .no-client-to-client-reflection=yes router-id=1.1.1.1 routing-table=main
/routing bgp connection
add as=64999 connect=yes disabled=no input.filter=antifilter-in listen=yes local.address=8.8.8.8 .role=ebgp multihop=yes name=geo-bgp output.filter-chain=discard .network=bgp-networks .no-client-to-client-reflection=\
    yes remote.address=1.1.1.1/32 .as=64998 .port=179 router-id=8.8.8.8 routing-table=main templates=geo-bgp.template
```

BIRD HINTS:

Show peers
---
```
birdc show protocol
```
Show routes
---
```
birdc show route
```

Recofigure after updates:
---
```
/usr/sbin/birdc configure
```
