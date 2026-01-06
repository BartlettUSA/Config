---
description: Generate Kubernetes deployment manifests
allowed-tools: Bash, Read, Write, Grep, Glob
model: sonnet
argument-hint: <app-name> [--type=deployment|service|ingress|all]
---

# /k8s-manifest — Kubernetes manifest generation

You are running the /k8s-manifest workflow.

## Inputs
- $ARGUMENTS: Application name plus optional type
  - `--type=deployment` - Deployment only
  - `--type=service` - Service only
  - `--type=ingress` - Ingress only
  - `--type=all` - Complete manifest set (default)
  - `--namespace=<ns>` - Target namespace

## Hard constraints
- Use latest stable API versions
- Include resource limits
- Set security contexts
- Add health probes
- Use ConfigMaps/Secrets for configuration

## Manifest templates

### Deployment
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: <app-name>
  namespace: <namespace>
  labels:
    app: <app-name>
spec:
  replicas: 3
  selector:
    matchLabels:
      app: <app-name>
  template:
    metadata:
      labels:
        app: <app-name>
    spec:
      securityContext:
        runAsNonRoot: true
        runAsUser: 1000
        fsGroup: 1000
      containers:
        - name: <app-name>
          image: <image>:<tag>
          ports:
            - containerPort: 8080
          resources:
            requests:
              memory: "128Mi"
              cpu: "100m"
            limits:
              memory: "256Mi"
              cpu: "500m"
          livenessProbe:
            httpGet:
              path: /health
              port: 8080
            initialDelaySeconds: 10
            periodSeconds: 10
          readinessProbe:
            httpGet:
              path: /ready
              port: 8080
            initialDelaySeconds: 5
            periodSeconds: 5
          securityContext:
            allowPrivilegeEscalation: false
            readOnlyRootFilesystem: true
```

### Service
```yaml
apiVersion: v1
kind: Service
metadata:
  name: <app-name>
  namespace: <namespace>
spec:
  selector:
    app: <app-name>
  ports:
    - port: 80
      targetPort: 8080
  type: ClusterIP
```

### Ingress
```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: <app-name>
  namespace: <namespace>
  annotations:
    kubernetes.io/ingress.class: nginx
    cert-manager.io/cluster-issuer: letsencrypt-prod
spec:
  tls:
    - hosts:
        - <app-name>.example.com
      secretName: <app-name>-tls
  rules:
    - host: <app-name>.example.com
      http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: <app-name>
                port:
                  number: 80
```

### HorizontalPodAutoscaler
```yaml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
  name: <app-name>
  namespace: <namespace>
spec:
  scaleTargetRef:
    apiVersion: apps/v1
    kind: Deployment
    name: <app-name>
  minReplicas: 2
  maxReplicas: 10
  metrics:
    - type: Resource
      resource:
        name: cpu
        target:
          type: Utilization
          averageUtilization: 70
```

## Process
1. Parse $ARGUMENTS for app name and options
2. Detect project type (for port, health paths)
3. Generate requested manifests
4. Validate with `kubectl --dry-run`
5. Write to `k8s/` directory

## Output format
### Kubernetes Manifests: <app-name>

**Namespace**: <namespace>
**Type**: <deployment|service|ingress|all>

#### Files Generated
| File | Kind | Description |
|------|------|-------------|
| k8s/deployment.yaml | Deployment | <replicas> replicas |
| k8s/service.yaml | Service | ClusterIP on port 80 |
| k8s/ingress.yaml | Ingress | TLS enabled |
| k8s/hpa.yaml | HPA | 2-10 replicas |

#### Validation
```bash
kubectl apply --dry-run=client -f k8s/
```

#### Apply Command
```bash
kubectl apply -f k8s/ -n <namespace>
```
