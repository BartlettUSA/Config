# /k8s-manifest — Generate Kubernetes manifests

You are running the /k8s-manifest workflow.

## Inputs
Use the user's message as app name plus optional type:
- `--type=deployment` - Deployment only
- `--type=service` - Service only
- `--type=ingress` - Ingress only
- `--type=all` - Complete set (default)
- `--namespace=<ns>` - Target namespace

## Hard constraints
- Use latest stable API versions
- Include resource limits
- Set security contexts
- Add health probes
- Use ConfigMaps/Secrets for configuration

## Generated manifests

### Deployment
- Security context (non-root, read-only fs)
- Resource requests and limits
- Liveness and readiness probes
- Pod anti-affinity

### Service
- ClusterIP type
- Port mapping

### Ingress
- TLS enabled
- cert-manager integration

### HPA
- CPU-based autoscaling
- 2-10 replicas

## Output format
### Kubernetes Manifests: <app-name>

| File | Kind |
|------|------|
| k8s/deployment.yaml | Deployment |
| k8s/service.yaml | Service |
| k8s/ingress.yaml | Ingress |
| k8s/hpa.yaml | HPA |

#### Apply Command
```bash
kubectl apply -f k8s/ -n <namespace>
```
