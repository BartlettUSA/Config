# /docker-optimize — Container optimization

You are running the /docker-optimize workflow.

## Inputs
Use the user's message for Dockerfile path (default: ./Dockerfile)
- `--analyze` - Analysis only
- `--fix` - Apply recommended fixes

## Hard constraints
- Maintain functionality while optimizing
- Use multi-stage builds where applicable
- Never use `:latest` tag in production
- Run as non-root user
- Include health checks

## Optimization strategies

### Base image selection
| Use case | Recommended |
|----------|-------------|
| Minimal | Alpine (5MB) |
| Security | Distroless |
| Node.js | node:20-alpine |
| Python | python:3.12-slim |

### Layer optimization
- Combine RUN commands
- Order from least to most frequently changing
- Clean up in same layer

### Security hardening
- Create non-root user
- Use read-only filesystem
- Pin specific versions

## Output format
### Docker Optimization: <dockerfile>

| Metric | Before | After |
|--------|--------|-------|
| Size | <n>MB | <n>MB |
| Layers | <n> | <n> |

#### Issues Found
| Severity | Issue | Fix |
|----------|-------|-----|
| 🔴 | | |

#### Optimized Dockerfile
```dockerfile
<if --fix>
```
