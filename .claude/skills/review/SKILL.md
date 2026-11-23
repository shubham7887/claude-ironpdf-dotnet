\---

name: review

description: Review my uncommitted changes before I commit. Use when I ask for a review or ask if something is ready to commit.

\---



\# Review my changes



1\. Run git diff and git diff --staged to see what changed. Don't edit any files.

2\. Check every change against this list:

&#x20;  - Does it do only what was asked? List anything extra.

&#x20;  - Edge cases: null, empty, zero, negative, very large input.

&#x20;  - Error handling: what happens when a call fails?

&#x20;  - Tests: is the new behavior covered? Does any test only check "not null"?

&#x20;  - Security: secrets in code, SQL built from strings, user input used without checks.

&#x20;  - The rules in CLAUDE.md.

3\. Reply with a short list, most important first:

&#x20;  \[must fix] file:line - what and why

&#x20;  \[should fix] file:line - what and why

&#x20;  \[nit] file:line - what and why

4\. End with one line: "Ready to commit" or "Not ready - fix the must-fix items first".

