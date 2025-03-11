# Create Branch Bash Utilities

A collection of utility scripts for streamlining Git workflows with JIRA tickets. These scripts help maintain consistent branch naming conventions and automate ticket-related workflows.

## Quick Setup

For a fresh installation, follow these steps:

#### 1. Install dependencies

```bash
# Install Homebrew if not already installed
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Install jq (required for ticket prefix configuration)
brew install jq
```

#### 2. Configure your JIRA ticket prefix

```bash
# Register the ticket prefix for your project
ticket_prefix -r TICKET
```

#### 3. Create your first branch

```bash
# Copy a JIRA ticket URL or description to clipboard
# Then create a branch based on clipboard content
create_branch
```

## Available Scripts

- **create_branch** - Creates a properly formatted Git branch from JIRA ticket information
- **create_branch_name** - Generates standardized branch names from JIRA ticket information
- **extract_ticket** - Extracts JIRA ticket numbers from clipboard or text input
- **ticket_prefix** - Manages project-specific JIRA ticket prefixes

## Workflow Overview

These scripts work together to automate branch creation based on JIRA tickets:

1. **Configure** your project's ticket prefix using `ticket_prefix`
2. **Extract** ticket numbers from text or clipboard using `extract_ticket`
3. **Generate** standardized branch names with `create_branch_name`
4. **Create** Git branches with proper naming using `create_branch`

## Detailed Script Documentation

### ticket_prefix

Manages JIRA project prefixes for different directories.

```bash
# View the current ticket prefix for this directory
ticket_prefix

# Register a prefix for the current directory
ticket_prefix -r TICKET
```

Features:
- Stores configuration in `~/.ticket.config` in JSON format
- Supports directory-specific prefixes
- Inherits prefixes from parent directories if not set locally
- Requires the `jq` command for JSON processing

### extract_ticket

Extracts JIRA ticket numbers from text input.

```bash
# Extract from clipboard
extract_ticket

# Extract from string argument
extract_ticket "Fix TICKET-12345 bug"

# Extract from piped input
echo "TICKET-12345 needs review" | extract_ticket
```

Features:
- Automatically detects the configured ticket prefix
- Checks command-line arguments, stdin, and clipboard in that order
- Extracts the first matching ticket number

### create_branch_name

Generates standardized branch names from ticket information.

```bash
# Generate feature branch name from clipboard
create_branch_name

# Generate bugfix branch name
create_branch_name --bugfix

# Generate custom prefix branch name
create_branch_name --prefix hotfix

# Include descriptive text in branch name
echo "TICKET-12345 needs review" | create_branch_name
# Output: feature/TICKET-12345-needs-review
```

Features:
- Creates branch names in format: `type/TICKET-NUMBER[-description]`
- Extracts descriptive text from input when available
- Sanitizes and formats branch names following best practices
- Supports feature, bugfix, and custom branch types

### create_branch

Creates and checks out Git branches with standardized naming.

```bash
# Create branch from current HEAD
create_branch

# Create branch from origin/develop
create_branch --develop

# Create bugfix branch
create_branch --bugfix

# Create branch with custom prefix
create_branch --prefix hotfix
```

Features:
- Combines branch name generation with Git operations
- Checks if branch already exists before creating
- Optionally creates branches from origin/develop
- Accepts all options from create_branch_name

## Installation

1. Ensure all scripts are in your PATH
2. Make sure scripts have executable permissions (`chmod +x script_name`)
3. Configure your ticket prefix with `ticket_prefix -r YOUR_PREFIX`

## Requirements

- Bash shell environment
- Git command-line tools
- `jq` for JSON processing (used by ticket_prefix)
- macOS `pbpaste` command for clipboard access

### Installing jq

If you don't have jq installed, you can easily install it using Homebrew:

```bash
# Install Homebrew if not already installed
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Install jq
brew install jq
```

You can verify the installation by running:

```bash
jq --version
```

## Code Style

See [CLAUDE.md](CLAUDE.md) for detailed code style guidelines and workflow documentation.