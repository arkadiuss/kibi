---
"kibi-cli": patch
---

`kibi check --staged` no longer grows with the square of the knowledge base. When a staged file changes a symbol, the check projects the branch's every entity and relationship into a throwaway KB in batches, and the Prolog wrapper appended `kb_save` to every mutating batch, rewriting the whole store each time. That KB lives and dies in one process and is never read back from disk, so it now asks for no saving (`PrologProcess` option `persistMutations: false`). On a KB of about 14,000 symbols, a five-line staged diff went from over 15 minutes (stopped unfinished) to 29 seconds.
