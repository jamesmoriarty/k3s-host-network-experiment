# k3s-host-network-experiment

## Results

| strategy | cni     | notes  |
|----------|---------|--------|
| default  | flannel | local* |
| exec     | flannel | local* |

\* can access locally on host ip e.g. http://10.0.0.238:8200/ 

## Capture

```
tshark -f "udp port 1900"
```

## Discovery

```
nmap -sU -p 1900 --script=upnp-info 10.0.0.0/24
```

```
upnp_info.py
```