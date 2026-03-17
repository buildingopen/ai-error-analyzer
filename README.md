# AI Error Analyzer

**6 copy-paste rules that reduce wasted AI retries by 34%.** Based on 5,890 real errors across 2,068 Claude Code sessions.

## The Problem

When AI coding agents hit an error, they handle it poorly:

- **49% of the time**, the AI retries the exact same failed action
- **Only 16% of the time**, it tries a different approach
- **57% of all errors** are preventable with better instructions

## The Rules

Copy these into your AI's instruction file:

| Tool | Where to paste |
|------|---------------|
| **Claude Code** | `CLAUDE.md` in your project root |
| **Cursor** | `.cursorrules` in your project root |
| **GitHub Copilot** | `.github/copilot-instructions.md` |
| **Windsurf** | `.windsurfrules` in your project root |
| **Other** | System prompt or custom instructions |

```markdown
## Error Recovery

1. After 2 failures with the same tool, stop. Try a completely different tool or approach. Do not retry a third time.
2. If a command is blocked or rejected, never retry it. It will fail again. Find another way immediately.
3. Before reading a file, verify it exists. Before editing a file, read it first.
4. If a file is too large to read, don't retry. Search for the specific content you need, or read a specific section using offset and limit.
5. Never run tasks in parallel if one depends on another. When one parallel task fails, all others get cancelled automatically. Run dependent steps one at a time.
6. After 3 total failures on any task, stop completely. Explain what failed and why. Do not keep going.
```

### Quick Start (Claude Code)

```bash
curl -sL https://raw.githubusercontent.com/buildingopen/ai-error-analyzer/main/rules.md >> CLAUDE.md
```

Or just copy the 6 rules above into your `CLAUDE.md`.

## Results

Measured across the same codebase, before and after adding these rules:

| Metric | Before | After | Change |
|--------|--------|-------|--------|
| Error recovery rate | 15.9% | 21.4% | +34% relative |
| Futile retries | 50.7% | 43.2% | -15% |
| Hook errors (blocked command retries) | 105 | 0 | -100% |
| File-too-large recovery | 7.1% | 32.1% | +352% |
| Network error recovery | 15.1% | 34.4% | +128% |

The overall recovery rate went from 15.9% to 21.4%. Some categories improved dramatically (hook errors dropped to zero, file-too-large recovery 4x'd). But the AI still retries uselessly 43% of the time. Instruction-level rules help, but they can't fully rewire model behavior.

## Run Your Own Analysis

This repo includes `analyze.py`, the same script that produced these findings. Point it at your Claude Code sessions and get a personalized error report.

**Requirements:** Python 3.10+ (standard library only, no pip install needed).

```bash
git clone https://github.com/buildingopen/ai-error-analyzer.git
cd ai-error-analyzer
python3 analyze.py
```

This scans `~/.claude/projects/` (where Claude Code stores session data) and writes `error-report.md` with your error taxonomy, retry rates, and recommendations.

### Options

```
python3 analyze.py --help
python3 analyze.py --sessions-dir /path/to/sessions    # Custom session directory
python3 analyze.py --output my-report.md               # Custom output file
```

### What it does

1. Reads every `.jsonl` session file in your Claude Code projects directory
2. Classifies each error into one of 14 categories (file not found, command failed, edit failed, etc.)
3. Tracks what happens after each error (retry, switch approach, give up, ask user)
4. Identifies which errors were preventable and how
5. Writes a markdown report with tables, stats, and recommendations

## Files

| File | What it is |
|------|-----------|
| `analyze.py` | The analysis script. Run it on your own Claude Code sessions. |
| `rules.md` | The 6 error recovery rules, ready to copy into your instruction file. |
| `EXAMPLE-REPORT.md` | Example output from running `analyze.py` on 2,068 sessions. Shows what your report will look like. |
| `LICENSE` | MIT |

## The Data Behind the Rules

| Stat | Value |
|------|-------|
| Total errors analyzed | 5,890 |
| Sessions analyzed | 2,068 |
| Preventable errors | 57% |
| Worst retry loop: same file read consecutively | 18 times |
| Worst session: tokens wasted on retries | 5.3M |

Full analysis methodology: [buildingopen/transcript-analyzer](https://github.com/buildingopen/transcript-analyzer)

## License

MIT
