# /doc-generate — Generate documentation from code

You are running the /doc-generate workflow.

## Inputs
Use the user's message as target path plus optional type:
- `--type=api` - OpenAPI/Swagger spec
- `--type=jsdoc` - JSDoc/TSDoc comments
- `--type=readme` - README with examples
- `--type=all` - All types

## Hard constraints
- Extract from actual code, don't invent
- Follow existing doc style if present
- Include practical examples
- Keep docs close to code

## Documentation types

### API documentation (OpenAPI)
Generate from route definitions with endpoints, methods, parameters, schemas

### JSDoc/TSDoc comments
```typescript
/**
 * Brief description.
 * @param {string} name - Description
 * @returns {Promise<Result>} Description
 * @example
 * const result = await fn('test');
 */
```

### README structure
- Installation, Quick Start, API Reference, Configuration

## Process
1. Find route definitions or exported functions
2. Extract endpoints/parameters/types
3. Identify request/response schemas
4. Generate documentation
5. Add examples from tests if available

## Output format
### Documentation Generated

| File | Type | Coverage |
|------|------|----------|
| docs/openapi.yaml | API | <n> endpoints |
| README.md | README | <sections> |

#### Undocumented Items
<list>

#### Preview Command
```bash
npx swagger-ui docs/openapi.yaml
```
