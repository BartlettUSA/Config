---
description: Generate API docs, JSDoc, TypeDoc from code
allowed-tools: Bash, Read, Write, Grep, Glob
model: sonnet
argument-hint: <path> [--type=api|jsdoc|readme|all]
---

# /doc-generate — Generate documentation from code

You are running the /doc-generate workflow.

## Inputs
- $ARGUMENTS: Target path plus optional type
  - `--type=api` - OpenAPI/Swagger spec
  - `--type=jsdoc` - JSDoc/TSDoc comments
  - `--type=readme` - README with examples
  - `--type=all` - All documentation types

## Hard constraints
- Extract from actual code, don't invent
- Follow existing doc style if present
- Include practical examples
- Keep docs close to code

## Documentation types

### 1. API documentation (OpenAPI)
```yaml
openapi: 3.0.3
info:
  title: <API Name>
  version: 1.0.0
paths:
  /endpoint:
    get:
      summary: <description>
      parameters:
        - name: id
          in: path
          required: true
          schema:
            type: string
      responses:
        '200':
          description: Success
          content:
            application/json:
              schema:
                $ref: '#/components/schemas/Response'
```

### 2. JSDoc/TSDoc comments
```typescript
/**
 * Brief description of the function.
 *
 * @param {string} name - Description of name parameter
 * @param {Options} options - Configuration options
 * @returns {Promise<Result>} Description of return value
 * @throws {ValidationError} When input is invalid
 *
 * @example
 * const result = await myFunction('test', { retry: true });
 * console.log(result.data);
 */
```

### 3. README structure
```markdown
# Project Name

Brief description.

## Installation

\`\`\`bash
npm install package-name
\`\`\`

## Quick Start

\`\`\`javascript
// Basic usage example
\`\`\`

## API Reference

### `functionName(params)`

Description and parameters.

## Configuration

Available options.

## Contributing

How to contribute.
```

## Process

### For API docs:
1. Find route definitions (Express, FastAPI, etc.)
2. Extract endpoints, methods, parameters
3. Identify request/response schemas
4. Generate OpenAPI spec
5. Add examples from tests if available

### For JSDoc:
1. Find exported functions/classes
2. Analyze parameter types
3. Infer return types
4. Extract existing comments
5. Generate/enhance documentation

### For README:
1. Analyze package.json/pyproject.toml
2. Find main entry points
3. Extract usage patterns from tests
4. Document configuration options
5. Add installation steps

## Output format
### Documentation Generated

**Target**: <path>
**Type**: <api|jsdoc|readme|all>

#### Files Created/Updated
| File | Type | Coverage |
|------|------|----------|
| docs/openapi.yaml | API | <n> endpoints |
| src/*.ts | JSDoc | <n> functions |
| README.md | README | <sections> |

#### API Endpoints (if applicable)
| Method | Path | Description |
|--------|------|-------------|
| GET | /users | List users |

#### Undocumented Items
<list of items needing manual documentation>

#### Next Steps
1. Review generated docs
2. Add missing descriptions
3. Verify examples work
4. Run doc linter

#### Preview Command
```bash
# Preview API docs
npx swagger-ui-express docs/openapi.yaml

# Build TypeDoc
npx typedoc --out docs src/
```
