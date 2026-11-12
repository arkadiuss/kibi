---
"kibi-cli": patch
---

A query that passes its client timeout now reports the state of its SWI-Prolog process after Kibi has stopped it. The message used to be built before the stop and read `killed=no, exitCode=null`, which looked like a process still running and a wedged engine, although Kibi had already stopped it and the engine starts a fresh session for the next request.

The timeout error no longer carries a `killed=` field. It says whether the process was stopped (with its exit code and signal) or did not stop after SIGTERM and SIGKILL, and the "engine state is likely wedged" hint is reduced to a pointer to `kibi engine stop`.
