## Cost-Optimized Task Routing

When executing tasks via /smart-build, follow these routing principles:

### Parallel dispatch (all conditions met):
- Subtasks touch different files
- No shared state or dependencies between them
- Can be validated independently

### Sequential dispatch (any condition):
- Subtask B needs output from subtask A
- Shared files between subtasks
- Integration step needed after independent work

### Cost targets:
- Aim for 60%+ of subtasks routed to junior-dev or mid-dev
- Track estimated cost savings vs running everything on opus