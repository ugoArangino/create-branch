# Create Branch Bash Utilities Guide

## Commands
- No formal build/lint/test commands - these are standalone Bash utilities

## Code Style Guidelines
- Use shebang `#!/usr/bin/env bash` for scripts
- Start with `set -euo pipefail` for defensive coding
- Set `IFS=$'\n\t'` for better whitespace handling
- Use lowercase_with_underscores for variable/function names
- Add usage() function for script documentation
- Use meaningful error messages with appropriate exit codes
- Include comments explaining non-obvious logic
- Implement defensive checks for required conditions and parameters
- Use double quotes around variables to prevent word splitting
- For inputs, check arguments first, then stdin, then clipboard
- Follow command-line conventions with both short (-h) and long (--help) options
- Structure scripts with logical sections (parsing, validation, main logic)

## Git Workflow
- Branch naming: `feature/TICKET-XXXXX` or `bugfix/TICKET-XXXXX`
- Always prefix branches with appropriate type (feature, bugfix, hotfix)
- JIRA tickets follow TICKET-XXXXX format