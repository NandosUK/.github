# NandosUK Claude Code Review

Add AI-powered code reviews to your repository using Claude.

## Setup (2 minutes)

### 1. Add Workflow File

```bash
mkdir -p .github/workflows
curl -o .github/workflows/claude-pr-review.yml \
  https://raw.githubusercontent.com/NandosUK/.github/main/templates/claude-pr-review-template.yml
```

### 2. Test It Works

Create a test PR with `@claude` in the description, or comment `@claude help` on any PR.

## Usage

Use `@claude` anywhere:
- **In PR description** → Reviews automatically when PR opens/updates
- **In PR comments** → Reviews on-demand
- **In issue comments** → Reviews related PR (if exists)

Examples:
- `@claude review this for security issues`
- `@claude help optimize this function`
- `@claude check coding standards`

## Optional: Custom Configuration

### Project Instructions
Create `CLAUDE.md` in your repository root for project-specific guidance:

```markdown
# Claude Instructions

## Build Commands
- `npm test` - Run tests
- `npm run lint` - Check code style

## Focus Areas
- Check database queries for N+1 issues
- Validate API security
- Ensure proper error handling
```

### PR Size Limits
Create `.claude-config.yml` in your repository root to customize limits:

```yaml
limits:
  max_files_changed: 25
  max_lines_changed: 1500
  max_diff_size_kb: 200
  max_file_size_kb: 50

file_types:
  include:
    - "*.js"
    - "*.ts"
    - "*.py"
  exclude:
    - "node_modules/**"
    - "*.min.js"
```

## Troubleshooting

**Claude doesn't respond?**
- Check workflow file exists in `.github/workflows/`
- Verify you used `@claude` in PR body or comments
- Check GitHub Actions logs for errors

**PR too large?**
- Claude skips PRs > 25 files or > 1500 lines
- Break large PRs into smaller chunks
- Check `.claude-config.yml` for custom limits

**Need help?** Ask in `#engineering-tools` Slack channel.