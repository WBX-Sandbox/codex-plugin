---
name: sandbox-workflows
description: Use WBX Sandbox to run code, keep project files between chats and hand off longer work as background jobs. Use when the user wants code actually executed, data analysed with real tools, files created or converted, a small web app served on a link, or a long task run without waiting.
---

# Working with WBX Sandbox

WBX Sandbox gives you an isolated Linux computer (a microVM) that belongs to the signed-in user's WBX account. Use it whenever running real code gives a better answer than describing what code would do.

## Pick the right way to run things

- **A quick command or snippet** (seconds to a minute): create or reuse a sandbox, then run the command or the code in it. Read the exit code and the output before answering.
- **Work longer than about a minute, or many independent tasks**: start a background job (or a batch of jobs) instead of keeping a command open. It returns an ID at once; wait for it, then read its summary, and fetch the log or result files only if they are needed.
- **Files**: write and read files directly instead of echoing large content through shell commands. Absolute paths under `/home/user` are a good default.
- **A web page or API the user should open**: start it in the background listening on `0.0.0.0`, then get the public HTTPS link for that port. Tell the user that anyone with the link can open it while the sandbox runs.

## Keep the user's work

- When the user works on a project they will come back to, create the sandbox with a short **name** (for example `sales-report`). A later chat that uses the same name gets the same sandbox and its files back.
- An idle sandbox falls asleep instead of being deleted; its files are kept and the next command wakes it. Do not recreate a sandbox only because it was asleep.
- Delete a sandbox only when the user asks for it or clearly no longer needs it – deleting removes its files.

## Be careful with cost and side effects

- Sandboxes and jobs use the user's paid compute. Do not start more sandboxes or jobs than the task needs, and prefer one sandbox per project.
- For jobs, set a price limit when the user mentions a budget; a job that could exceed it is refused before it starts.
- Commands, file writes and deletions change the sandbox. Before deleting files or sandboxes, make sure that is what the user wants.
- Sandboxes have internet access by default, but private networks and outgoing e-mail (SMTP) are blocked. Do not try to work around these limits.

## Report results honestly

- Summarise what ran and what came out: the exit code, the important lines of output, and where result files are.
- If a command fails, show the relevant error and either fix the cause or explain what the user can do. Never present an unrun or failed step as successful.
- If a tool reports that the account is paused, out of credit or over a limit, tell the user plainly; they manage their account at sandbox.wbx.cz.
