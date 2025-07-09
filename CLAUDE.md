# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This is the **NandosUK Claude Code Review System** - a centralized repository containing GitHub workflows and templates for AI-powered code reviews using Claude across all NandosUK repositories.

### Architecture
- **Centralized Reusable Workflows**: Main workflow orchestration with built-in safety checks in `.github/workflows/`
- **Template System**: Simple templates in `templates/` directory for easy repository adoption
- **Organization-wide Standards**: Centralized instructions in `INSTRUCTIONS.md`
- **Instruction Hierarchy**: Organization standards → Repository-specific `CLAUDE.md` → Auto-detected context
- **Production Safety**: Built-in PR size limits, file filtering, and smart review strategies

### Key Components
- **claude-reusable.yml**: Main reusable workflow with built-in safety checks
- **claude-pr-review-template.yml**: Simple workflow template for repositories
- **advanced-workflow-template.yml**: Template with custom timeout/turns configuration
- **INSTRUCTIONS.md**: Organization-wide coding standards and review criteria
- **CLAUDE-template.md**: Template for repository-specific instructions
- **.claude-config.yml**: Template for customizing PR limits and review strategies

## Usage Patterns

### Workflow Integration
Individual repositories use these workflows by:
1. Copying workflow template to their `.github/workflows/`
2. Optionally creating repository-specific `CLAUDE.md` files
3. Using `@claude` trigger:
   - In PR body → Automatic review on PR open/sync/reopen
   - In PR/issue comments → Manual review trigger

### Claude Interaction Flow
```
@claude (PR body or comment) → Workflow trigger → Reusable workflow → AI processing
```

### Template Usage
- `templates/claude-pr-review-template.yml`: Basic setup - just copy and use
- `templates/advanced-workflow-template.yml`: With custom timeout and conversation limits
- `templates/CLAUDE-template.md`: Template for repository-specific instructions
- `templates/.claude-config.yml`: Template for customizing PR limits and review strategies

## Key Configuration

### Required Permissions
Workflows need these permissions in target repositories:
- `contents: write` - Read repository files
- `issues: write` - Comment on issues  
- `pull-requests: write` - Comment on PRs
- `id-token: write` - OIDC token for auth

### Organization Secrets (Pre-configured)
- `ANTHROPIC_API_KEY`: Claude API access
- `CLAUDE_APP_ID`: GitHub App ID  
- `CLAUDE_APP_PRIVATE_KEY`: GitHub App private key

### Trigger Patterns
- `@claude` in PR body: Triggers on PR opened/synchronize/reopened
- `@claude` in PR comments: Manual trigger for PR review comments
- `@claude` in issue comments: Manual trigger for issue comments (only if issue has associated PR)

### PR Safety Limits
- **Max files changed**: 25
- **Max lines changed**: 1500 (insertions + deletions)
- **Max diff size**: 200KB
- **Max file size**: 50KB per file
- **Review strategies**: detailed → security-and-bugs → summary-only → skip

## File Structure Understanding

### Critical Files
- `INSTRUCTIONS.md`: Organization-wide standards (security, code quality, architecture)
- `README.md`: Complete documentation and setup guide
- `templates/`: Reusable workflow and instruction templates

### Standards Enforcement
The `INSTRUCTIONS.md` file contains comprehensive standards for:
- **Security**: Input validation, secrets management, authentication
- **Code Quality**: TypeScript patterns, error handling, logging
- **Architecture**: API design, database guidelines, testing requirements
- **Performance**: Database optimization, API response times, caching

## Development Commands

This repository primarily contains configuration files and templates, so typical development commands would be:

```bash
# Validate workflow syntax
yamllint .github/workflows/*.yml templates/*.yml

# Check markdown formatting
markdownlint *.md templates/*.md

# Test workflow templates (in target repositories)
gh workflow run "claude-pr-review.yml"
```

## Review Focus Areas

When working with this repository:

### Template Quality
- Ensure workflow templates are syntactically correct
- Verify secret references and workflow triggers
- Check conditional logic for Claude mentions

### Documentation Consistency
- Keep README.md and INSTRUCTIONS.md synchronized
- Ensure templates match documented patterns
- Validate example code in documentation

### Standards Maintenance
- Review and update organization coding standards
- Ensure security best practices are current
- Update technology preferences and approved libraries

## Common Usage Scenarios

### Adding New Repository
1. Copy workflow template to repository
2. Create repository-specific `CLAUDE.md` if needed
3. Test with `@claude help` comment

### Updating Organization Standards
1. Modify `INSTRUCTIONS.md` with new standards
2. Update templates if workflow changes needed
3. Communicate changes to development teams

### Troubleshooting
- Check workflow logs in target repository's Actions tab
- Verify organization secrets are properly configured
- Ensure `@claude` mentions are properly formatted