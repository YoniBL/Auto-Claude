# Prompt Variable Naming Conventions

This document defines the standard variable naming conventions for all prompt files in `apps/backend/prompts/`. All prompts MUST follow these conventions for consistency and maintainability.

## Standard Conventions

### Directory Variables: UPPER_CASE

Directory paths and environment constants should use **UPPER_CASE with underscores**:

```bash
SPEC_DIR="./auto-claude/specs/YOUR-SPEC-NAME"  # Spec directory path
PROJECT_ROOT="."                                # Project root directory
WORKING_DIR="."                                 # Current working directory
MEMORY_DIR="./memory"                           # Memory directory path
```

**Examples:**
- ✅ `SPEC_DIR` - Correct
- ✅ `PROJECT_ROOT` - Correct
- ❌ `spec_dir` - Incorrect (use UPPER_CASE)
- ❌ `SpecDir` - Incorrect (use UPPER_CASE with underscores)

### File Path Variables: snake_case

File paths and file-related variables should use **snake_case**:

```bash
file_path="./path/to/file"                      # File path variable
spec_file="./spec.md"                           # Specific file
plan_file="./implementation_plan.json"          # Plan file path
context_file="./context.json"                   # Context file path
```

**Examples:**
- ✅ `file_path` - Correct
- ✅ `spec_file` - Correct
- ❌ `FILE_PATH` - Incorrect (use snake_case for files)
- ❌ `filePath` - Incorrect (use snake_case, not camelCase)

### Constants: UPPER_CASE

Constants and configuration values should use **UPPER_CASE**:

```bash
PROJECT_ROOT="."                                # Constants
MAX_RETRIES=3                                   # Numeric constants
DEFAULT_PORT=8000                               # Default values
```

### Python Variables: snake_case

When using variables in Python code snippets within prompts, use **snake_case**:

```python
spec_dir = Path.cwd()  # Python variable
file_path = "./spec.md"
current_subtask = subtask
```

**Note:** Python variables follow Python conventions (snake_case), even when referencing directories.

## Quoting Styles

### Bash Variables

Always use **double quotes** for bash variables to handle paths with spaces:

```bash
cat "$SPEC_DIR/implementation_plan.json"  # ✅ Correct
cat $SPEC_DIR/implementation_plan.json   # ❌ Incorrect (no quotes)
cat '$SPEC_DIR/implementation_plan.json'  # ❌ Incorrect (single quotes prevent expansion)
```

### File Paths in Examples

When showing example paths (not actual variables), use backticks for markdown formatting:

```markdown
Read the file at `./path/to/file.md`
Check `spec.md` for requirements
```

## Variable Declaration Patterns

### Bash Variables

```bash
# Set directory variable
SPEC_DIR="./auto-claude/specs/YOUR-SPEC-NAME"

# Set file variable
file_path="./path/to/file"

# Use with quotes
cat "$SPEC_DIR/implementation_plan.json"
cat "$file_path"
```

### Python Variables

```python
# Directory variables (snake_case in Python)
spec_dir = Path.cwd()
memory_dir = Path("memory")

# File variables
file_path = "./spec.md"
plan_file = "implementation_plan.json"
```

## Common Variable Names

### Standard Directory Variables

| Variable | Purpose | Example |
|----------|---------|---------|
| `SPEC_DIR` | Spec directory path | `SPEC_DIR="./auto-claude/specs/my-spec"` |
| `PROJECT_ROOT` | Project root directory | `PROJECT_ROOT="."` |
| `WORKING_DIR` | Current working directory | `WORKING_DIR="."` |
| `MEMORY_DIR` | Memory directory path | `MEMORY_DIR="./memory"` |

### Standard File Variables

| Variable | Purpose | Example |
|----------|---------|---------|
| `file_path` | Generic file path | `file_path="./path/to/file"` |
| `spec_file` | Spec file path | `spec_file="./spec.md"` |
| `plan_file` | Implementation plan file | `plan_file="./implementation_plan.json"` |
| `context_file` | Context file path | `context_file="./context.json"` |

## Migration Checklist

When updating prompts to follow these conventions:

1. ✅ Replace `spec_dir` (lowercase) with `SPEC_DIR` (uppercase) in bash
2. ✅ Replace `FILE_PATH` (uppercase) with `file_path` (snake_case) for file variables
3. ✅ Ensure all bash variables use double quotes: `"$SPEC_DIR"`
4. ✅ Keep Python variables in snake_case: `spec_dir = Path.cwd()`
5. ✅ Use UPPER_CASE for directory constants
6. ✅ Use snake_case for file path variables

## Examples

### ✅ Correct Usage

```bash
# Directory variable (UPPER_CASE)
SPEC_DIR="./auto-claude/specs/my-spec"
cat "$SPEC_DIR/implementation_plan.json"

# File variable (snake_case)
file_path="./path/to/file"
cat "$file_path"

# Python (snake_case)
spec_dir = Path.cwd()
file_path = "./spec.md"
```

### ❌ Incorrect Usage

```bash
# Wrong: lowercase directory variable
spec_dir="./auto-claude/specs/my-spec"  # ❌

# Wrong: uppercase file variable
FILE_PATH="./path/to/file"  # ❌

# Wrong: no quotes
cat $SPEC_DIR/file  # ❌

# Wrong: camelCase
filePath="./path/to/file"  # ❌
```

## Enforcement

- All new prompts MUST follow these conventions
- PR reviews should verify variable naming consistency
- Use `grep` to search for old patterns before committing

## Search Patterns for Verification

To verify compliance, search for:

```bash
# Find old patterns
grep -r "spec_dir\|file_path\|FILE_PATH" apps/backend/prompts/

# Should find only:
# - SPEC_DIR (correct)
# - file_path (correct)
# - spec_dir in Python code (correct)
```

