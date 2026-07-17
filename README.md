# bambuddy-k8s

Kubernetes manifests for [Bambuddy](https://bambuddy.cool) ([source](https://github.com/maziggy/bambuddy)), deployed via ArgoCD.

Runs `hostNetwork: true` pinned to `pop-4` — Bambuddy needs SSDP multicast for
printer discovery, same trade-off as `network_mode: host` in the upstream
docker-compose file.

Served at https://bambuddy.monashautomation.com via the cluster's existing
Traefik ingress + Cloudflare Tunnel.

Config (printers, plates, settings) is restored via Bambuddy's own
GitHub-backup restore feature in-app, not tracked in this repo.

## Local apply

```bash
kubectl apply -k manifests/
```
