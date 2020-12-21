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
upnp_info.py
```