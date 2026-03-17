# AI Error Recovery Rules

**6 rules that took my AI's error recovery rate from 16% to 67%.**

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

| Metric | Before | After |
|--------|--------|-------|
| Error recovery rate | 16% | 67% |
| Futile retries | 49% | ~12% |
| Cascade failures | 23% | ~8% |

Same AI. Same tasks. Six sentences.

## The Data

These rules came from analyzing 5,890 errors across 2,068 AI coding sessions using [transcript-analyzer](https://github.com/buildingopen/transcript-analyzer).

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
