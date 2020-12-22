# k3s-host-network-experiment

Why did my minidlna setup stop working?

## Commands

```
bin/k3s/uninstall
```

```
bin/k3s/<cni>/<strategy>/install
```

## Matrix

| cni      | config  | notes  |
|----------|---------|--------|
| flannel  | default |        |
| flannel  | custom  | `INSTALL_K3S_EXEC="--disable-network-policy --no-deploy traefik --bind-address=$(bin/ip) --node-ip=$(bin/ip) --node-external-ip=$(bin/ip) --cluster-cidr=192.168.0.0/16 --service-cidr=192.168.0.0/16"` |
| none     | custom  | `INSTALL_K3S_EXEC="--flannel-backend=none --no-flannel --disable-network-policy --no-deploy traefik"` |
| cilium   | default | `INSTALL_K3S_EXEC="--flannel-backend=none --no-flannel --disable-network-policy --no-deploy traefik"` |


### Debug

```
ss -lntp | grep -E ':(8200) '
```

### Capture

```
tshark -f "udp port 1900"
```

### Discovery

```
nmap -sU -p 1900 --script=upnp-info 10.0.0.0/24
```

## Notes

- udp/upnp broadcast/advertisement on 1900.
- tcp/http serve on 8200. 
- can generally access internally from host ip e.g. http://10.0.0.238:8200/
- external port block on :8200? iptables, ufw, ...
- [k3s installer options](https://rancher.com/docs/k3s/latest/en/advanced/#starting-the-server-with-the-installation-script)

