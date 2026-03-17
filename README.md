# AI Error Recovery Rules

**6 rules based on 5,890 real AI coding errors. They help. They're not enough.**

Based on 5,890 real errors across 2,068 coding sessions. [Full analysis](https://github.com/buildingopen/transcript-analyzer).

## The Problem

- 49% of the time, AI retries the exact same failed action without changing anything
- Only 16% of the time, it tries a different approach
- 57% of all errors are completely preventable

## The Rules

Copy these into your AI's instruction file.

| Tool | File |
|------|------|
| Claude Code | `CLAUDE.md` in project root |
| Cursor | `.cursorrules` in project root |
| Copilot | `.github/copilot-instructions.md` |
| Windsurf | `.windsurfrules` in project root |
| Other | System prompt or custom instructions |

### Error Recovery

1. **After 2 failures with the same tool, stop.** Try a completely different tool or approach. Do not retry a third time.

2. **If a command is blocked or rejected, never retry it.** It will fail again. Find another way immediately.

   > **Example: Claude Code hooks.** If you use stop hooks (like secret scanning or destructive command blocking), the AI will retry the blocked command 68.9% of the time. Hooks are deterministic: if it blocked once, it blocks every time. Every retry is guaranteed to fail.

3. **Before reading a file, verify it exists. Before editing a file, read it first.** This alone prevents 12% of all errors.

4. **If a file is too large to read, don't retry.** Search for the specific content you need, or read a specific section using offset and limit.

5. **Never run tasks in parallel if one depends on another.** When one parallel task fails, all others get cancelled automatically. Run dependent steps one at a time.

6. **After 3 total failures on any task, stop completely.** Explain what failed and why. Do not keep going.

## Results

| Metric | Before Rules | After Rules |
|--------|-------------|-------------|
| Error recovery rate | 15.9% | 21.4% |
| Futile retries | 50.7% | 43.2% |
| Hook errors | 105 | 0 |
| File-too-large recovery | 7.1% | 32.1% |
| Network error recovery | 15.1% | 34.4% |

Some categories improved dramatically. Overall recovery improved 34% relative. But the AI still retries 43% of the time. Instruction-level rules can't fully rewire model behavior.

## Run Your Own Analysis

This repo includes `analyze.py`, the script that generated these findings. Point it at your Claude Code sessions and get your own error report.

```bash
git clone https://github.com/buildingopen/ai-error-rules.git
cd ai-error-rules
python3 analyze.py
```

It reads your session files from `~/.claude/projects/` and outputs a full error taxonomy with recovery rates, retry loops, and wasted tokens.

## The Data

| Finding | Number |
|---------|--------|
| Total errors analyzed | 5,890 |
| Sessions analyzed | 2,068 |
| Preventable errors | 57% |
| Worst retry: same file read consecutively | 18 times |
| Worst session: tokens wasted on retries | 5.3M |

## Quick Start

**Claude Code:**
```bash
echo '## Error Recovery

1. After 2 failures with the same tool, stop. Try a completely different tool or approach. Do not retry a third time.
2. If a command is blocked or rejected, never retry it. It will fail again. Find another way immediately.
3. Before reading a file, verify it exists. Before editing a file, read it first.
4. If a file is too large to read, don't retry. Search for the specific content you need, or read a specific section using offset and limit.
5. Never run tasks in parallel if one depends on another. When one parallel task fails, all others get cancelled automatically. Run dependent steps one at a time.
6. After 3 total failures on any task, stop completely. Explain what failed and why. Do not keep going.' >> CLAUDE.md
```

## License

MIT
