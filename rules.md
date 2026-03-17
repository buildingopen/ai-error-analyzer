## Error Recovery

1. After 2 failures with the same tool, stop. Try a completely different tool or approach. Do not retry a third time.
2. If a command is blocked or rejected, never retry it. It will fail again. Find another way immediately.
3. Before reading a file, verify it exists. Before editing a file, read it first.
4. If a file is too large to read, don't retry. Search for the specific content you need, or read a specific section using offset and limit.
5. Never run tasks in parallel if one depends on another. When one parallel task fails, all others get cancelled automatically. Run dependent steps one at a time.
6. After 3 total failures on any task, stop completely. Explain what failed and why. Do not keep going.
