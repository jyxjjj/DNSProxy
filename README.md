# DNS Proxy

Quadlet files for DNS Proxy.

## Description

- If you are in China, use `src/China` to as `/`
- If you are not in China, use `src/Global` to as `/`

## Usage

```
systemctl daemon-reload
systemctl start dnsproxy.service
```

## Architecture

The global architecture is:

![Global](architecture.png)

## Notice
This Pod can only allow dns queries from `127.0.0.1`.

Due to `SystemD-Resolved` already listening on `127.0.0.53:53`,
we didn't use `0.0.0.0` to publish the ports.

### Intranet Sharing

If you want to share it to intranet,
you should add lines to main container file `dnsproxy-main.container`:

```systemd-unit
PublishPorts={IntranetIPAddress}:53:53/tcp
PublishPorts={IntranetIPAddress}:53:53/udp
```

### Internet Sharing

If you want to share it to intranet,
you should add lines to main container file `dnsproxy-main.container`:

```systemd-unit
PublishPorts={InternetIPAddress}:53:53/tcp
PublishPorts={InternetIPAddress}:53:53/udp
```


# License

- [AGPL-3.0-only](https://www.gnu.org/licenses/agpl-3.0.html)

# Thanks to

- [AdguardTeam/dnsproxy](https://github.com/AdguardTeam/dnsproxy)
- [containers/podman](https://github.com/containers/podman)
