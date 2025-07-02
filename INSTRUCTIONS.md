# NandosUK Organization Claude Instructions

> These instructions apply to all repositories in the NandosUK organization.
> Repository-specific instructions in CLAUDE.md will supplement these standards.

## Security Standards (Critical)

### Never Commit Secrets
- **API Keys**: Use environment variables, never hard-code
- **Passwords**: Hash and salt, store securely
- **Tokens**: Use secure storage, rotate regularly
- **Connection Strings**: Environment variables only
- **Private Keys**: Never in source code

### Input Validation
- **All user inputs** must be validated and sanitized
- **SQL Injection**: Use parameterized queries only
- **XSS Prevention**: Escape output, validate input
- **File Uploads**: Validate type, size, scan for malware
- **API Parameters**: Type checking, length limits

### Authentication & Authorization
- **JWT Tokens**: Proper expiration, secure signing
- **API Keys**: Rate limiting, scope restrictions
- **Session Management**: Secure cookies, timeout
- **OAuth2**: Follow best practices, validate scopes
- **Role-Based Access**: Principle of least privilege

## Code Quality Standards

### TypeScript/JavaScript
```typescript
// Prefer explicit types
interface User {
  id: string;
  email: string;
  createdAt: Date;
}

// Use proper error handling
try {
  const result = await api.call();
  return result;
} catch (error) {
  logger.error('API call failed', { error: error.message });
  throw new APIError('External service unavailable');
}
```

### Error Handling
```javascript
// Standard error response format
{
  "success": false,
  "error": "VALIDATION_ERROR",
  "message": "Invalid email format",
  "details": {
    "field": "email",
    "code": "INVALID_FORMAT"
  },
  "timestamp": "2024-01-01T12:00:00Z"
}
```

### Logging Standards
```javascript
// Use structured logging
logger.info('User created', {
  userId: user.id,
  email: user.email,
  source: 'registration'
});

// Never log sensitive data
logger.info('Login attempt', {
  userId: user.id,
  // password: user.password  ❌ Never do this
  success: true
});
```

## Architecture Patterns

### API Design
- **RESTful**: Use proper HTTP methods and status codes
- **Versioning**: `/api/v1/`, `/api/v2/` in URL path
- **Rate Limiting**: Implement for all public endpoints
- **Documentation**: OpenAPI/Swagger for all APIs
- **Health Checks**: `/health` endpoint for monitoring

### Database Guidelines
```sql
-- Use parameterized queries
SELECT * FROM users WHERE id = $1 AND status = $2;

-- Proper indexing
CREATE INDEX idx_users_email ON users(email);
CREATE INDEX idx_orders_user_created ON orders(user_id, created_at);

-- Naming conventions
-- Tables: snake_case (users, order_items)
-- Columns: snake_case (created_at, user_id)
-- Constraints: descriptive names (fk_orders_user_id)
```

### Testing Requirements
- **Unit Tests**: 80%+ coverage minimum
- **Integration Tests**: API endpoints, database operations
- **E2E Tests**: Critical user journeys
- **Security Tests**: Input validation, auth flows
- **Performance Tests**: Load testing for APIs

## Technology Preferences

### Approved Libraries
- **HTTP Client**: axios (Node.js), requests (Python)
- **Validation**: joi, zod (Node.js), pydantic (Python)
- **Testing**: jest, vitest (Node.js), pytest (Python)
- **Database**: Prisma, TypeORM (Node.js), SQLAlchemy (Python)
- **Authentication**: passport.js, next-auth (Node.js)

### Avoid These
- **Direct SQL**: Use ORM/query builder
- **Synchronous Operations**: Use async/await
- **Global Variables**: Use dependency injection
- **Hardcoded URLs**: Use configuration
- **console.log**: Use proper logging library

## Performance Standards

### Database Optimization
- **Query Performance**: N+1 queries, proper joins
- **Connection Pooling**: Don't create new connections per request
- **Caching**: Redis for frequently accessed data
- **Pagination**: Limit/offset or cursor-based
- **Indexing**: Analyze slow query log

### API Performance
- **Response Time**: < 200ms for simple queries
- **Compression**: gzip/brotli for responses
- **Caching Headers**: Appropriate cache-control
- **Asset Optimization**: CDN for static files
- **Bundle Size**: Keep JavaScript bundles < 250KB

## Deployment & Operations

### Environment Management
```bash
# Required environment variables
NODE_ENV=production
DATABASE_URL=postgresql://...
REDIS_URL=redis://...
LOG_LEVEL=info
API_VERSION=v1.2.3
```

### Health Monitoring
```javascript
// Health check endpoint
app.get('/health', async (req, res) => {
  const checks = {
    database: await checkDatabase(),
    redis: await checkRedis(),
    external_api: await checkExternalAPI()
  };
  
  const isHealthy = Object.values(checks).every(check => check.status === 'ok');
  
  res.status(isHealthy ? 200 : 503).json({
    status: isHealthy ? 'healthy' : 'unhealthy',
    timestamp: new Date().toISOString(),
    checks
  });
});
```

### Security Headers
```javascript
// Required security headers
app.use((req, res, next) => {
  res.setHeader('X-Content-Type-Options', 'nosniff');
  res.setHeader('X-Frame-Options', 'DENY');
  res.setHeader('X-XSS-Protection', '1; mode=block');
  res.setHeader('Strict-Transport-Security', 'max-age=31536000');
  next();
});
```

## Review Criteria for Claude

When reviewing code, prioritize these areas:

### 🔴 Critical Issues (Must Fix)
1. **Security vulnerabilities** (secrets, injection, XSS)
2. **Performance problems** (N+1 queries, memory leaks)
3. **Data loss risks** (missing transactions, race conditions)
4. **Authentication bypasses** (missing auth, privilege escalation)

### 🟡 Important Issues (Should Fix)
1. **Error handling** (unhandled exceptions, poor logging)
2. **Code quality** (maintainability, readability)
3. **Testing gaps** (missing tests, poor coverage)
4. **Documentation** (missing docs, outdated comments)

### 🟢 Suggestions (Nice to Have)
1. **Code optimization** (minor performance improvements)
2. **Style consistency** (formatting, naming)
3. **Architecture improvements** (better patterns)
4. **Dependency updates** (security patches, features)

## Common Anti-Patterns to Flag

### ❌ Security Anti-Patterns
```javascript
// Hard-coded secrets
const API_KEY = "sk-1234567890abcdef";  // ❌

// Direct SQL concatenation
const query = `SELECT * FROM users WHERE id = ${userId}`;  // ❌

// Exposing internal errors
res.status(500).send(error.stack);  // ❌
```

### ❌ Performance Anti-Patterns
```javascript
// N+1 query problem
for (const user of users) {
  const orders = await db.query('SELECT * FROM orders WHERE user_id = ?', user.id);  // ❌
}

// Synchronous operations
const data = fs.readFileSync('./large-file.json');  // ❌

// Memory leaks
const cache = {};  // Never cleared ❌
```

### ❌ Code Quality Anti-Patterns
```javascript
// Magic numbers
setTimeout(callback, 86400000);  // ❌ What is 86400000?

// Deep nesting
if (user) {
  if (user.active) {
    if (user.permissions) {
      if (user.permissions.includes('admin')) {  // ❌ Too deep
        // ...
      }
    }
  }
}

// Unclear variable names
const d = new Date();  // ❌
const u = await getUser();  // ❌
```

---

*Last updated: 2024-01-01*  
*Maintained by: NandosUK DevOps Team*