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

## Updates

The Bambuddy version is pinned (tag + digest) in `manifests/kustomization.yaml`. Renovate
(`renovate.json`) opens a PR for each new upstream release once it's 3 days old; patch and minor
releases merge automatically, majors wait for a review. Argo deploys whatever is merged. Don't use
Bambuddy's in-app updater: it changes code inside the running container, which is lost on restart.
