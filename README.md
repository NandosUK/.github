# NandosUK Claude Code Review System

This repository contains centralized GitHub workflows for AI-powered code reviews using Claude across all NandosUK repositories.

## 🚀 Quick Start

### 1. Add to Your Repository

Copy the workflow file to your repository:

```bash
# Create the directory
mkdir -p .github/workflows

# Copy the template
curl -o .github/workflows/claude-pr-review.yml \
  https://raw.githubusercontent.com/NandosUK/.github/main/templates/claude-pr-review-template.yml
```

### 2. Start Using Claude

In any PR, issue, or comment, mention Claude:

```
@claude review this PR for security issues
@claude help me optimize this function
@claude check if this follows our coding standards
```

## 📋 How It Works

### Architecture

```
Individual Repo Workflow → Centralized Reusable Workflow → Claude Code Action
     (trigger)                    (orchestration)              (AI processing)
```

### Instruction Hierarchy

1. **Organization Standards** (`INSTRUCTIONS.md`) - Applied to all repos
2. **Repository Instructions** (`CLAUDE.md`) - Project-specific rules
3. **Auto-detected Context** - Technology stack, build tools, etc.

## 🛠️ Setup Requirements

### Organization Secrets (Already Configured)

- `ANTHROPIC_API_KEY` - Claude API access
- `CLAUDE_APP_ID` - GitHub App ID
- `CLAUDE_APP_PRIVATE_KEY` - GitHub App private key

### Repository Setup

1. **Copy workflow file** (see Quick Start)
2. **Optional**: Create repository-specific `CLAUDE.md` file
3. **Test**: Create a PR and comment `@claude help`

## 📝 Repository Instructions (Optional)

Create a `CLAUDE.md` file in your repository root for project-specific guidance:

```markdown
# My Project Claude Instructions

## Project Context
- This is a Node.js API service
- Uses PostgreSQL database
- Deployed on AWS ECS

## Specific Review Areas
- Check database query performance
- Validate API security
- Ensure proper error handling

## Build Commands
- `npm run test` - Run tests
- `npm run lint` - Check code style
- `npm run build` - Build for production
```

## 💡 Usage Examples

### Code Review
```
@claude review this PR for:
- Security vulnerabilities
- Performance issues
- Code style compliance
- Missing tests
```

### Code Assistance
```
@claude help me improve this function for better performance
@claude suggest better error handling for this API endpoint
@claude check if this database query can be optimized
```

### Architecture Guidance
```
@claude does this follow our microservices patterns?
@claude review this API design for RESTful best practices
@claude check if this component structure is maintainable
```

## ⚙️ Configuration Options

### Workflow Customization

```yaml
# In your repository's .github/workflows/claude-pr-review.yml
uses: NandosUK/.github/.github/workflows/claude-reusable.yml@main
with:
  instructions_url: 'https://raw.githubusercontent.com/NandosUK/.github/main/INSTRUCTIONS.md'  # Custom org instructions
```

### Supported Events

- `issue_comment` - Comments on issues
- `pull_request_review_comment` - PR review comments  
- `issues` - New issues opened/assigned

## 📊 Features

### ✅ What Claude Can Do

- **Security Analysis**: Detect vulnerabilities, secrets exposure
- **Code Quality**: Style, maintainability, best practices
- **Performance Review**: Database queries, algorithms, caching
- **Architecture Guidance**: Design patterns, structure recommendations
- **Testing Suggestions**: Coverage, test quality, edge cases
- **Documentation**: Code comments, API documentation

### ⚠️ Limitations

- **60-minute timeout** per interaction
- **5 conversation turns** maximum
- **Requires `@claude` mention** to trigger
- **Context limited** to repository contents

## 🔧 Troubleshooting

### Common Issues

**Claude doesn't respond**
- Check if `@claude` is mentioned in comment
- Verify workflow file exists in `.github/workflows/`
- Check organization secrets are configured

**Missing context**
- Ensure `CLAUDE.md` file is in repository root
- Check if organization `INSTRUCTIONS.md` is accessible
- Verify repository permissions

**Timeout errors**
- Break large requests into smaller parts
- Use specific, focused questions
- Check if repository is too large

### Getting Help

- **Slack**: `#engineering-tools` channel
- **Issues**: Create issue in this repository
- **Documentation**: Check workflow logs in Actions tab

## 📚 Templates

See the `templates/` directory for:
- `claude-pr-review-template.yml` - Basic workflow
- `CLAUDE-template.md` - Repository instructions template
- `advanced-workflow-template.yml` - Advanced configuration

## 🔄 Updates

This system is automatically updated. Your repositories will use the latest version unless you specify a specific version:

```yaml
uses: NandosUK/.github/.github/workflows/claude-reusable.yml@v1.0  # Pin to specific version
```

## 📈 Best Practices

### For Effective Reviews
1. **Be specific** in your requests
2. **Provide context** about requirements
3. **Ask focused questions** rather than broad reviews
4. **Include error messages** when debugging

### For Repository Setup
1. **Create CLAUDE.md** for project-specific guidance
2. **Include build commands** and testing instructions
3. **Document architecture patterns** and conventions
4. **Update instructions** as project evolves

---

*Last updated: $(date +%Y-%m-%d)*  
*Maintained by: DevOps Team*