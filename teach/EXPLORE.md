# Parallel explorers

For a subsystem too big to trace in one pass. Split the question into two to four **angles**, each a distinct slice (entry points, data model, a specific flow, the boundary with another service). Spawn one read-only explorer per angle, all in one message so they run in parallel.

Each explorer's brief: the question, its angle, "others cover the other slices; go deep on yours", and this return format:

- **Components**: each key type, module or function with its file path and one line on what it does.
- **Flow**: step by step, which function runs, in which file, what it calls next, and the data passed between steps.
- **Boundaries**: inputs and outputs where this slice meets the rest of the codebase.
- **Non-obvious things**: anything surprising or easy to get wrong.
- **Open questions**: what it couldn't trace.
- **Files read**: every file, so you can check claims.

When they return, merge the overlaps into one picture, settle contradictions by reading the code yourself, and carry their open questions into the page rather than papering over them.
