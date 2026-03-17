# Error Taxonomy Report

**Generated:** 2026-03-09 15:50
**Files processed:** 2068
**Files with errors:** 801
**Total errors:** 5890

## 1. Error Categories Overview

| Category | Count | % of Total | Description |
|----------|------:|----------:|-------------|
| `FILE_TOO_LARGE` | 173 | 2.9% | File exceeds size or token limits for Read tool |
| `FILE_NOT_READ` | 182 | 3.1% | Writing to a file without reading it first |
| `FILE_NOT_FOUND` | 696 | 11.8% | Attempting to read/edit files that do not exist |
| `HOOK_BLOCKED` | 106 | 1.8% | PreToolUse/PostToolUse hooks blocking operations |
| `USER_REJECTED` | 241 | 4.1% | User declined a proposed tool use |
| `EDIT_FAILED` | 47 | 0.8% | Edit operations with wrong old_string or ambiguous matches |
| `PERMISSION_DENIED` | 36 | 0.6% | OS-level or SSH permission failures |
| `NETWORK_ERROR` | 357 | 6.1% | Timeouts, connection refused, DNS failures |
| `TOOL_NOT_FOUND` | 84 | 1.4% | Calling tools/skills that do not exist |
| `SIBLING_ERROR` | 1370 | 23.3% | Parallel tool call cancelled due to sibling failure |
| `MCP_ERROR` | 115 | 2.0% | MCP server errors (Playwright refs, connection issues) |
| `COMMAND_FAILED` | 1958 | 33.2% | Bash commands returning non-zero exit codes |
| `TOOL_ERROR` | 32 | 0.5% | Generic tool execution errors |
| `UNKNOWN` | 493 | 8.4% | Uncategorized errors |

## 2. Per-Category Details

### FILE_TOO_LARGE

**Count:** 173 (2.9%)

**Example messages:**

1. `File content (27229 tokens) exceeds maximum allowed tokens (25000). Please use offset and limit parameters to read specific portions of the file, or use the GrepTool to search for specific content.`
2. `File content (36522 tokens) exceeds maximum allowed tokens (25000). Please use offset and limit parameters to read specific portions of the file, or use the GrepTool to search for specific content.`
3. `File content (1.2MB) exceeds maximum allowed size (256KB). Please use offset and limit parameters to read specific portions of the file, or use the GrepTool to search for specific content.`

**Sessions with most occurrences:**

| Session | Count |
|---------|------:|
| `4d4546b8-e12f-48f4-a140-...` | 18 |
| `e7d5896d-ce9a-49f0-bdd4-...` | 17 |
| `69d9805b-6486-4b28-af78-...` | 12 |

**Post-error behavior:**

| Action | Count | % |
|--------|------:|--:|
| retried_same_tool | 62 | 35.8% |
| asked_user | 52 | 30.1% |
| gave_up | 38 | 22.0% |
| switched_approach | 21 | 12.1% |

### FILE_NOT_READ

**Count:** 182 (3.1%)

**Example messages:**

1. `File has been modified since read, either by the user or by a linter. Read it again before attempting to write it.`
2. `File has not been read yet. Read it first before writing to it.`

**Sessions with most occurrences:**

| Session | Count |
|---------|------:|
| `e7d5896d-ce9a-49f0-bdd4-...` | 13 |
| `7b593199-af98-4cba-9d03-...` | 8 |
| `00b13b35-5e55-47d7-bd41-...` | 8 |

**Post-error behavior:**

| Action | Count | % |
|--------|------:|--:|
| switched_approach | 111 | 61.0% |
| retried_same_tool | 55 | 30.2% |
| asked_user | 12 | 6.6% |
| gave_up | 4 | 2.2% |

### FILE_NOT_FOUND

**Count:** 696 (11.8%)

**Example messages:**

1. `File does not exist. Note: your current working directory is /root/rocketlist-wt-const-comment.`
2. `Exit code 2 ls: cannot access '/root/rocketlist-minimal/agent-tests/': No such file or directory ls: cannot access '/root/rocketlist-minimal/agent-tests/': No such file or directory`
3. `File does not exist. Note: your current working directory is /root/queen.`

**Sessions with most occurrences:**

| Session | Count |
|---------|------:|
| `5e43b8d8-b89a-43e3-9448-...` | 72 |
| `17daff99-1111-425b-8a0f-...` | 33 |
| `e7d5896d-ce9a-49f0-bdd4-...` | 21 |

**Post-error behavior:**

| Action | Count | % |
|--------|------:|--:|
| retried_same_tool | 325 | 46.7% |
| switched_approach | 204 | 29.3% |
| gave_up | 84 | 12.1% |
| asked_user | 83 | 11.9% |

### HOOK_BLOCKED

**Count:** 106 (1.8%)

**Example messages:**

1. `PreToolUse:Bash hook error: [/root/.claude/hooks/scan-secrets-before-push.sh]: No stderr output`
2. `PreToolUse:Bash hook error: [/root/.claude/hooks/block-destructive.sh]: No stderr output`

**Sessions with most occurrences:**

| Session | Count |
|---------|------:|
| `edea9cba-68ee-4f34-9d90-...` | 13 |
| `34091837-1d4f-4293-afb7-...` | 10 |
| `d281abd6-d2ff-4f4c-886c-...` | 6 |

**Post-error behavior:**

| Action | Count | % |
|--------|------:|--:|
| retried_same_tool | 73 | 68.9% |
| gave_up | 14 | 13.2% |
| asked_user | 13 | 12.3% |
| switched_approach | 6 | 5.7% |

### USER_REJECTED

**Count:** 241 (4.1%)

**Example messages:**

1. `The user doesn't want to proceed with this tool use. The tool use was rejected (eg. if it was a file edit, the new_string was NOT written to the file). STOP what you are doing and wait for the user to...`
2. `Exit code 1 To https://github.com/federicodeponte/fedeponte.com.git ! [rejected] main -> main (fetch first) error: failed to push some refs to 'https://github.com/federicodeponte/fedeponte.com.git' hi...`
3. `Exit code 1 [fede-dev a47a05b] fix: 8 more audit issues (rate limiting, atomicity, timestamps, email links) 8 files changed, 65 insertions(+), 46 deletions(-) To https://github.com/openpaper-dev/openp...`

**Sessions with most occurrences:**

| Session | Count |
|---------|------:|
| `e7d5896d-ce9a-49f0-bdd4-...` | 10 |
| `4e134ec6-ddea-4659-9ec1-...` | 10 |
| `3bd60856-c247-44ee-8e78-...` | 9 |

**Post-error behavior:**

| Action | Count | % |
|--------|------:|--:|
| gave_up | 190 | 78.8% |
| retried_same_tool | 32 | 13.3% |
| asked_user | 19 | 7.9% |

### EDIT_FAILED

**Count:** 47 (0.8%)

**Example messages:**

1. `String to replace not found in file. String: ### Issue 73: No input validation on generation request parameters - **Status**: OPEN`
2. `String to replace not found in file. String: ### Issue 85: Password length not bounded before argon2 hashing - **Status**: OPEN`
3. `String to replace not found in file. String: ### Issue 111: Imprint page missing canonical URL - **Status**: OPEN`

**Sessions with most occurrences:**

| Session | Count |
|---------|------:|
| `00345d0d-62ce-48ef-a83f-...` | 3 |
| `15e2714d-5b3d-4c4d-95e8-...` | 3 |
| `d0cd7632-10cc-447e-8938-...` | 2 |

**Post-error behavior:**

| Action | Count | % |
|--------|------:|--:|
| switched_approach | 26 | 55.3% |
| retried_same_tool | 12 | 25.5% |
| asked_user | 6 | 12.8% |
| gave_up | 3 | 6.4% |

### PERMISSION_DENIED

**Count:** 36 (0.6%)

**Example messages:**

1. `Exit code 255 Warning: Permanently added '91.99.110.206' (ED25519) to the list of known hosts. root@91.99.110.206: Permission denied (publickey). Warning: Permanently added '91.99.110.206' (ED25519) t...`
2. `Exit code 255 root@91.99.110.206: Permission denied (publickey). root@91.99.110.206: Permission denied (publickey).`
3. `Exit code 255 Permission denied, please try again. Permission denied, please try again. root@65.21.90.216: Permission denied (publickey,password). Permission denied, please try again. Permission denie...`

**Sessions with most occurrences:**

| Session | Count |
|---------|------:|
| `630c4b93-8594-47a4-afcc-...` | 3 |
| `e7d5896d-ce9a-49f0-bdd4-...` | 3 |
| `44b8ddba-2a32-4562-b17d-...` | 3 |

**Post-error behavior:**

| Action | Count | % |
|--------|------:|--:|
| retried_same_tool | 21 | 58.3% |
| asked_user | 10 | 27.8% |
| gave_up | 5 | 13.9% |

### NETWORK_ERROR

**Count:** 357 (6.1%)

**Example messages:**

1. `Exit code 1 (node:160338) [DEP0169] DeprecationWarning: `url.parse()` behavior is not standardized and prone to errors that have security implications. Use the WHATWG URL API instead. CVEs are not iss...`
2. `Exit code 1 (node:163375) [DEP0169] DeprecationWarning: `url.parse()` behavior is not standardized and prone to errors that have security implications. Use the WHATWG URL API instead. CVEs are not iss...`
3. `Exit code 128 remote: Repository not found. fatal: repository 'https://github.com/openpaper-dev/openpaper.git/' not found remote: Repository not found. fatal: repository 'https://github.com/openpaper-...`

**Sessions with most occurrences:**

| Session | Count |
|---------|------:|
| `c694abf2-6ce0-46d9-a01c-...` | 33 |
| `4d4546b8-e12f-48f4-a140-...` | 22 |
| `fc87fd6b-9ec8-45a0-ad3a-...` | 21 |

**Post-error behavior:**

| Action | Count | % |
|--------|------:|--:|
| asked_user | 132 | 37.0% |
| retried_same_tool | 97 | 27.2% |
| gave_up | 70 | 19.6% |
| switched_approach | 58 | 16.2% |

### TOOL_NOT_FOUND

**Count:** 84 (1.4%)

**Example messages:**

1. `No task found with ID: ae4f3cf54a8d5d0cb`
2. `Error: No such tool available: mcp__authenticated-browser__browser_navigate`
3. `No task found with ID: ac06019ea5666720f`

**Sessions with most occurrences:**

| Session | Count |
|---------|------:|
| `d0cd7632-10cc-447e-8938-...` | 11 |
| `00345d0d-62ce-48ef-a83f-...` | 7 |
| `8d472cec-e526-4e46-a7c8-...` | 5 |

**Post-error behavior:**

| Action | Count | % |
|--------|------:|--:|
| switched_approach | 50 | 59.5% |
| retried_same_tool | 14 | 16.7% |
| gave_up | 11 | 13.1% |
| asked_user | 9 | 10.7% |

### SIBLING_ERROR

**Count:** 1370 (23.3%)

**Example messages:**

1. `Sibling tool call errored`

**Sessions with most occurrences:**

| Session | Count |
|---------|------:|
| `af7a823a-499a-4cee-8e53-...` | 102 |
| `d0cd7632-10cc-447e-8938-...` | 73 |
| `5e43b8d8-b89a-43e3-9448-...` | 66 |

**Post-error behavior:**

| Action | Count | % |
|--------|------:|--:|
| retried_same_tool | 790 | 57.7% |
| asked_user | 293 | 21.4% |
| switched_approach | 176 | 12.8% |
| gave_up | 111 | 8.1% |

### MCP_ERROR

**Count:** 115 (2.0%)

**Example messages:**

1. `### Error Error: Ref e81 not found in the current page snapshot. Try capturing new snapshot.`
2. `### Error Error: page._wrapApiCall: Execution context was destroyed, most likely because of a navigation`
3. `### Error Error: Ref e39 not found in the current page snapshot. Try capturing new snapshot.`

**Sessions with most occurrences:**

| Session | Count |
|---------|------:|
| `fc87fd6b-9ec8-45a0-ad3a-...` | 15 |
| `c694abf2-6ce0-46d9-a01c-...` | 10 |
| `8d472cec-e526-4e46-a7c8-...` | 8 |

**Post-error behavior:**

| Action | Count | % |
|--------|------:|--:|
| switched_approach | 74 | 64.3% |
| retried_same_tool | 18 | 15.7% |
| asked_user | 13 | 11.3% |
| gave_up | 10 | 8.7% |

### COMMAND_FAILED

**Count:** 1958 (33.2%)

**Example messages:**

1. `Exit code 127 /bin/bash: line 1: file: command not found /bin/bash: line 1: file: command not found`
2. `Exit code 1 can't find pane: q/rocket/theme can't find pane: q/rocket/theme`
3. `Exit code 1 Already on 'main' Your branch is up to date with 'origin/main'. Already up to date. merge: worker-10of10 - not something we can merge Did you mean this? origin/worker-10of10 CONFLICT Alrea...`

**Sessions with most occurrences:**

| Session | Count |
|---------|------:|
| `c694abf2-6ce0-46d9-a01c-...` | 102 |
| `d0cd7632-10cc-447e-8938-...` | 97 |
| `e7d5896d-ce9a-49f0-bdd4-...` | 90 |

**Post-error behavior:**

| Action | Count | % |
|--------|------:|--:|
| retried_same_tool | 1173 | 59.9% |
| asked_user | 495 | 25.3% |
| gave_up | 225 | 11.5% |
| switched_approach | 65 | 3.3% |

### TOOL_ERROR

**Count:** 32 (0.5%)

**Example messages:**

1. `InputValidationError: Grep failed due to the following issue: An unexpected parameter `file_path` was provided`
2. `InputValidationError: [ { "origin": "array", "code": "too_small", "minimum": 2, "inclusive": true, "path": [ "questions", 0, "options" ], "message": "Too small: expected array to have >=2 items" } ]`
3. `Bash command failed for pattern "```! "/root/.claude/plugins/cache/claude-plugins-official/ralph-loop/8deab8460a9d/scripts/setup-ralph-loop.sh" Port all missing interactivity from minimal.html to mini...`

**Sessions with most occurrences:**

| Session | Count |
|---------|------:|
| `17daff99-1111-425b-8a0f-...` | 3 |
| `69d9805b-6486-4b28-af78-...` | 2 |
| `d0cd7632-10cc-447e-8938-...` | 2 |

**Post-error behavior:**

| Action | Count | % |
|--------|------:|--:|
| retried_same_tool | 21 | 65.6% |
| switched_approach | 7 | 21.9% |
| gave_up | 2 | 6.2% |
| asked_user | 2 | 6.2% |

### UNKNOWN

**Count:** 493 (8.4%)

**Example messages:**

1. `### Error Error: dialog.accept: Protocol error (Page.handleJavaScriptDialog): No dialog is showing`
2. `EEXIST: file already exists, mkdir '/root/.claude/projects/-root/memory'`
3. `### Error Error: Access to "file:" URL is blocked. Allowed protocols: http:, https:, about:, data:. Attempted URL: file:///tmp/og-render.html`

**Sessions with most occurrences:**

| Session | Count |
|---------|------:|
| `2b66fd22-c240-45e4-b384-...` | 100 |
| `d0cd7632-10cc-447e-8938-...` | 44 |
| `af7a823a-499a-4cee-8e53-...` | 29 |

**Post-error behavior:**

| Action | Count | % |
|--------|------:|--:|
| retried_same_tool | 186 | 37.7% |
| switched_approach | 147 | 29.8% |
| asked_user | 98 | 19.9% |
| gave_up | 62 | 12.6% |

## 3. Error Sequences: What Happens After an Error?

Analysis of agent behavior immediately following an error.

| Action | Count | % of Total | Description |
|--------|------:|----------:|-------------|
| `retried_same_tool` | 2879 | 48.9% | Agent retried the same tool (possibly with different parameters) |
| `asked_user` | 1237 | 21.0% | Agent responded with text only (likely asking for guidance) |
| `switched_approach` | 945 | 16.0% | Agent used a different tool or strategy |
| `gave_up` | 829 | 14.1% | No further assistant action found in the chain |

### Retry Rates by Error Category

Which error types lead to retrying the same tool vs switching approach?

| Category | Retry Same | Switch | Ask User | Gave Up |
|----------|----------:|-------:|---------:|--------:|
| `FILE_TOO_LARGE` | 62 | 21 | 52 | 38 |
| `FILE_NOT_READ` | 55 | 111 | 12 | 4 |
| `FILE_NOT_FOUND` | 325 | 204 | 83 | 84 |
| `HOOK_BLOCKED` | 73 | 6 | 13 | 14 |
| `USER_REJECTED` | 32 | 0 | 19 | 190 |
| `EDIT_FAILED` | 12 | 26 | 6 | 3 |
| `PERMISSION_DENIED` | 21 | 0 | 10 | 5 |
| `NETWORK_ERROR` | 97 | 58 | 132 | 70 |
| `TOOL_NOT_FOUND` | 14 | 50 | 9 | 11 |
| `SIBLING_ERROR` | 790 | 176 | 293 | 111 |
| `MCP_ERROR` | 18 | 74 | 13 | 10 |
| `COMMAND_FAILED` | 1173 | 65 | 495 | 225 |
| `TOOL_ERROR` | 21 | 7 | 2 | 2 |
| `UNKNOWN` | 186 | 147 | 98 | 62 |

## 4. Errors by Tool

Which tools produce the most errors?

| Tool | Error Count | % of Identified |
|------|----------:|-----------:|
| `Bash` | 3192 | 54.3% |
| `Read` | 1132 | 19.2% |
| `WebFetch` | 284 | 4.8% |
| `Edit` | 204 | 3.5% |
| `Glob` | 186 | 3.2% |
| `Grep` | 170 | 2.9% |
| `ExitPlanMode` | 140 | 2.4% |
| `mcp__authenticated-browser__browser_navigate` | 103 | 1.8% |
| `Write` | 80 | 1.4% |
| `mcp__authenticated-browser__browser_click` | 68 | 1.2% |
| `mcp__authenticated-browser__browser_run_code` | 64 | 1.1% |
| `TaskOutput` | 51 | 0.9% |
| `WebSearch` | 31 | 0.5% |
| `AskUserQuestion` | 29 | 0.5% |
| `mcp__authenticated-browser__browser_take_screenshot` | 27 | 0.5% |

## 5. Preventable Errors

How many errors could have been avoided with different practices?

### Prevention Strategies

| Strategy | Errors Prevented | % of Total |
|----------|----------------:|----------:|
| Not easily preventable | 2526 | 42.9% |
| Better tool choice | 2379 | 40.4% |
| Checking before acting | 1078 | 18.3% |
| Better CLAUDE.md instructions | 467 | 7.9% |
| Reading the file first | 229 | 3.9% |

**Total preventable errors:** 3364 (57.1%)
**Not easily preventable:** 2526 (42.9%)

### Prevention by Category

| Category | Errors | Prevention Strategies |
|----------|------:|----------------------|
| `FILE_TOO_LARGE` | 173 | Better tool choice (173) |
| `FILE_NOT_READ` | 182 | Reading the file first (182) |
| `FILE_NOT_FOUND` | 696 | Checking before acting (696), Better tool choice (696) |
| `HOOK_BLOCKED` | 106 | Better CLAUDE.md instructions (106) |
| `USER_REJECTED` | 241 | Better CLAUDE.md instructions (241) |
| `EDIT_FAILED` | 47 | Reading the file first (47), Checking before acting (47) |
| `PERMISSION_DENIED` | 36 | Better CLAUDE.md instructions (36), Checking before acting (36) |
| `NETWORK_ERROR` | 357 | Not easily preventable (304), Checking before acting (53) |
| `TOOL_NOT_FOUND` | 84 | Better CLAUDE.md instructions (84) |
| `SIBLING_ERROR` | 1370 | Better tool choice (1370) |
| `MCP_ERROR` | 115 | Not easily preventable (115) |
| `COMMAND_FAILED` | 1958 | Not easily preventable (1582), Checking before acting (246), Better tool choice (140) |
| `TOOL_ERROR` | 32 | Not easily preventable (32) |
| `UNKNOWN` | 493 | Not easily preventable (493) |

## 6. Key Findings and Recommendations

### Top Error Sources

1. **COMMAND_FAILED** -- 1958 errors (33.2%)
2. **SIBLING_ERROR** -- 1370 errors (23.3%)
3. **FILE_NOT_FOUND** -- 696 errors (11.8%)
4. **UNKNOWN** -- 493 errors (8.4%)
5. **NETWORK_ERROR** -- 357 errors (6.1%)

### Actionable Recommendations

1. **Reduce COMMAND_FAILED errors:** Many bash command failures come from test suites and missing dependencies. Add CLAUDE.md instructions to check command availability before running, and use `which` or `command -v` to verify tools exist.

2. **Reduce FILE_NOT_FOUND errors:** Agent frequently tries to read files that do not exist. Add CLAUDE.md instruction: 'Always use Glob or ls to verify file paths before reading.'

3. **Reduce EDIT_FAILED errors:** String matching failures in Edit tool. Ensure the agent always reads the latest file content before editing, and uses more context in old_string for uniqueness.

4. **Reduce FILE_TOO_LARGE errors:** Agent attempts to read very large files. Add CLAUDE.md instruction: 'For files over 200KB, always use offset/limit or Grep instead of Read.'

5. **Reduce HOOK_BLOCKED errors:** Custom hooks are blocking operations the agent attempts. Review hook scripts and add clearer CLAUDE.md rules about restricted operations.

6. **Reduce USER_REJECTED errors:** The agent proposes actions the user declines. This may indicate the agent should ask for confirmation earlier in its reasoning, or CLAUDE.md constraints are not specific enough.

7. **Reduce SIBLING_ERROR errors:** Parallel tool calls fail as a cascade. Consider making dependent tool calls sequential, or validate inputs before batching.

8. **Reduce FILE_NOT_READ errors:** Agent writes without reading first. This is already enforced by the tool, but the agent still attempts it. Reinforce in CLAUDE.md: 'ALWAYS read a file before writing or editing it.'

