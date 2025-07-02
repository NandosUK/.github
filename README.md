# NandosUK Organization GitHub Configuration

Organization-wide GitHub workflows and configurations for **Nando's UK**.

## 🤖 Claude AI Code Review

Claude AI is integrated across all repositories for automated code review and assistance.

### How to Use

Mention `@claude` in any issue or pull request comment:

```markdown
@claude review this PR for security issues

@claude help me understand this code

@claude suggest improvements for this function

@claude check for performance issues
```

### What Claude Does

- **Security Reviews** - Identifies vulnerabilities and security issues
- **Code Quality** - Checks best practices and coding standards  
- **Performance Analysis** - Suggests optimizations
- **Bug Detection** - Finds potential issues
- **Code Explanation** - Explains complex code sections

### Response Time

Claude typically responds in **30-90 seconds**. Check the Actions tab if no response appears.

## Repository Structure

```
.github/
├── .github/workflows/
│   └── claude-organization-wide.yml    # Claude integration
└── README.md                          # This file
```

## Usage Examples

**Security Review:**
```
@claude review this authentication code for security vulnerabilities
```

**Code Quality:**
```
@claude check if this follows TypeScript best practices
```

**Bug Help:**
```
@claude this function is throwing an error, can you help debug it?
```

**Performance:**
```
@claude suggest optimizations for this database query
```

---

*Organization-wide Claude integration - automatically available in all repositories*
