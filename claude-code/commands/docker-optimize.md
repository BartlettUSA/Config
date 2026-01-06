---
description: Container optimization and Dockerfile best practices
allowed-tools: Bash, Read, Write, Edit, Grep, Glob
model: sonnet
argument-hint: [Dockerfile path] [--analyze | --fix]
---

# /docker-optimize — Container optimization

You are running the /docker-optimize workflow.

## Inputs
- $ARGUMENTS: Optional Dockerfile path (default: ./Dockerfile)
  - `--analyze` - Analysis only, no changes
  - `--fix` - Apply recommended fixes

## Hard constraints
- Maintain functionality while optimizing
- Use multi-stage builds where applicable
- Never use `:latest` tag in production
- Run as non-root user
- Include health checks

## Optimization categories

### 1. Base image selection
| Use case | Recommended | Size |
|----------|-------------|------|
| Minimal | Alpine | 5MB |
| Security | Distroless | 2-20MB |
| Node.js | node:20-alpine | 50MB |
| Python | python:3.12-slim | 45MB |
| Go | scratch | 0MB |

### 2. Layer optimization
```dockerfile
# BAD: Multiple RUN commands
RUN apt-get update
RUN apt-get install -y curl
RUN apt-get clean

# GOOD: Combined RUN command
RUN apt-get update && \
    apt-get install -y --no-install-recommends curl && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*
```

### 3. Multi-stage build pattern
```dockerfile
# Build stage
FROM node:20-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production
COPY . .
RUN npm run build

# Production stage
FROM node:20-alpine
WORKDIR /app
COPY --from=builder /app/dist ./dist
COPY --from=builder /app/node_modules ./node_modules
USER node
CMD ["node", "dist/index.js"]
```

### 4. Security hardening
```dockerfile
# Create non-root user
RUN addgroup -g 1001 appgroup && \
    adduser -u 1001 -G appgroup -s /bin/sh -D appuser
USER appuser

# Read-only filesystem
# (set in docker-compose or runtime)
```

### 5. Caching optimization
```dockerfile
# Order from least to most frequently changing
COPY package*.json ./
RUN npm ci
COPY tsconfig.json ./
COPY src ./src
RUN npm run build
```

### 6. Health check
```dockerfile
HEALTHCHECK --interval=30s --timeout=3s --start-period=5s --retries=3 \
  CMD wget --no-verbose --tries=1 --spider http://localhost:3000/health || exit 1
```

## Analysis checks
| Check | Issue | Fix |
|-------|-------|-----|
| Base image | Using :latest | Pin specific version |
| Root user | Running as root | Add USER directive |
| Layer count | Too many layers | Combine RUN commands |
| No .dockerignore | Large context | Create .dockerignore |
| No health check | No liveness probe | Add HEALTHCHECK |
| Secrets in image | Credentials in ENV | Use secrets mount |

## Process
1. Read Dockerfile (or find it)
2. Analyze current state:
   - Image size estimate
   - Layer count
   - Security issues
3. Generate recommendations
4. If `--fix`, apply changes
5. Show before/after comparison

## Output format
### Docker Optimization: <dockerfile>

#### Current State
| Metric | Value |
|--------|-------|
| Base image | <image> |
| Estimated size | <size> |
| Layer count | <n> |
| Build stages | <n> |

#### Issues Found
| Severity | Issue | Line | Fix |
|----------|-------|------|-----|
| 🔴 Critical | | | |
| 🟡 Warning | | | |
| 🔵 Info | | | |

#### Recommendations
1. <recommendation with code example>

#### Optimized Dockerfile
```dockerfile
<optimized version if --fix>
```

#### Expected Improvements
| Metric | Before | After | Change |
|--------|--------|-------|--------|
| Size | <n>MB | <n>MB | -<n>% |
| Layers | <n> | <n> | -<n> |
| Build time | <n>s | <n>s | -<n>% |
