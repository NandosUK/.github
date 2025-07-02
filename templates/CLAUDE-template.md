# Claude Instructions for [REPOSITORY_NAME]

> This file provides repository-specific guidance to Claude for code reviews and assistance.
> These instructions supplement the organization-wide standards.

## Project Overview

### Technology Stack
- **Language**: [e.g., TypeScript, Python, Java]
- **Framework**: [e.g., Express.js, FastAPI, Spring Boot]
- **Database**: [e.g., PostgreSQL, MongoDB, Redis]
- **Deployment**: [e.g., AWS ECS, GCP Cloud Run, Kubernetes]

### Architecture
- **Type**: [e.g., Microservice, Monolith, Serverless]
- **Patterns**: [e.g., Clean Architecture, MVC, Domain-Driven Design]
- **Key Components**: 
  - Component 1: Brief description
  - Component 2: Brief description

## Build & Test Commands

```bash
# Development
npm run dev              # Start development server
npm run build            # Build for production

# Testing
npm run test             # Run all tests
npm run test:unit        # Run unit tests only
npm run test:integration # Run integration tests
npm run test:e2e         # Run end-to-end tests

# Code Quality
npm run lint             # Check code style
npm run format           # Format code
npm run type-check       # TypeScript type checking
```

## Review Focus Areas

### Security
- [Specific security concerns for this project]
- [Authentication/authorization patterns to check]
- [Data validation requirements]

### Performance
- [Database query optimization]
- [Caching strategies]
- [API response time requirements]

### Code Quality
- [Naming conventions specific to this project]
- [Error handling patterns]
- [Logging requirements]

## Project-Specific Patterns

### Data Access
```javascript
// Example: Preferred database access pattern
const result = await db.query('SELECT * FROM users WHERE id = $1', [userId]);
```

### Error Handling
```javascript
// Example: Standard error response format
res.status(400).json({
  error: 'VALIDATION_ERROR',
  message: 'Invalid input provided',
  details: validationErrors
});
```

### Authentication
```javascript
// Example: How auth should be implemented
const token = req.headers.authorization?.replace('Bearer ', '');
const user = await verifyToken(token);
```

## Dependencies & Libraries

### Approved Libraries
- **HTTP Client**: axios (preferred)
- **Validation**: joi / zod
- **Testing**: jest / vitest
- **Linting**: eslint + prettier

### Avoid
- [Libraries to avoid and why]
- [Deprecated patterns]

## Common Issues to Watch For

1. **[Issue 1]**: [Description and how to fix]
2. **[Issue 2]**: [Description and how to fix]
3. **[Issue 3]**: [Description and how to fix]

## API Standards

### Request/Response Format
```json
{
  "success": true,
  "data": {},
  "message": "Optional success message"
}
```

### Error Format
```json
{
  "success": false,
  "error": "ERROR_CODE",
  "message": "Human readable message",
  "details": {}
}
```

## Database Guidelines

### Naming Conventions
- Tables: `snake_case`
- Columns: `snake_case`
- Indexes: `idx_table_column`

### Migration Patterns
- Always use migrations for schema changes
- Include rollback instructions
- Test migrations on staging first

## Deployment Considerations

### Environment Variables
```bash
# Required environment variables
DATABASE_URL=postgresql://...
API_KEY=...
LOG_LEVEL=info
```

### Health Checks
- Endpoint: `/health`
- Response: `{ "status": "healthy", "timestamp": "..." }`

## Claude Usage Examples

### For this repository, use commands like:
```
@claude review this API endpoint for security and performance
@claude check if this database query follows our optimization patterns
@claude validate this error handling against our standards
@claude ensure this component follows our architecture patterns
```

## Additional Resources

- [Link to internal documentation]
- [Architecture diagrams]
- [API documentation]
- [Deployment guides]

---

*Last updated: [DATE]*
*Review and update this file as the project evolves*