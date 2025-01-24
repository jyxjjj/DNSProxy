# DNS Proxy

Quadlet files for DNS Proxy.

## Description

- If you are in China, use `src/China` to as `/`
- If you are not in China, use `src/Global` to as `/`

## Usage

China:

```
systemctl daemon-reload
systemctl start dnsproxy-network.service
systemctl start dnsproxy-upstream-main.service
systemctl start dnsproxy-upstream-fallback.service
systemctl start dnsproxy.service
```

Global:

```
systemctl daemon-reload
systemctl start dnsproxy-network.service
systemctl start dnsproxy-upstream-main-google.service
systemctl start dnsproxy-upstream-main-cloudflare.service
systemctl start dnsproxy-upstream-main.service
systemctl start dnsproxy-upstream-fallback-google.service
systemctl start dnsproxy-upstream-fallback-cloudflare.service
systemctl start dnsproxy-upstream-fallback.service
systemctl start dnsproxy.service
```

## Architecture

The `Global`'s architecture is:

![Global](architecture.png)

## Notice
This Pod can only allow dns queries from `127.0.0.1`.

Due to `SystemD-Resolved` already listening on `127.0.0.53:53`,
we didn't use `0.0.0.0` to publish the ports.

### Intranet Sharing

If you want to share it to intranet,
you should add overrides to main container file `dnsproxy.container` via `dnsproxy.container.d/00-intranet.conf`:

```systemd-unit
[Container]
PublishPorts={IntranetIPAddress}:53:53/tcp
PublishPorts={IntranetIPAddress}:53:53/udp
```

### Internet Sharing

If you want to share it to intranet,
you should add overrides to main container file `dnsproxy.container` via `dnsproxy.container.d/01-intranet.conf`:

```systemd-unit
[Container]
PublishPorts={InternetIPAddress}:53:53/tcp
PublishPorts={InternetIPAddress}:53:53/udp
```


# License

- [AGPL-3.0-only](https://www.gnu.org/licenses/agpl-3.0.html)

# Thanks to

- [AdguardTeam/dnsproxy](https://github.com/AdguardTeam/dnsproxy)
- [containers/podman](https://github.com/containers/podman)
