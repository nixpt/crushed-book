# Agent Knowledge Graph System (AKGS)

> "The Long-Term Memory for AI Agents."

AKGS is a native graph database embedded in the Crush Runtime. It allows agents to store structured knowledge (Nodes and Edges) rather than just flat files.

## Data Model

AKGS uses a semantic triple-like structure:

*   **Nodes**: Entities (e.g., `User`, `Task`, `File`).
*   **Edges**: Relationships (e.g., `ASSIGNED_TO`, `DEPENDS_ON`).
*   **Properties**: Key-Value pairs attached to nodes/edges.

## Usage

Access AKGS via the standard library:

```python
# Create a node
user_id = akg.create_node("User", {"name": "Alice"})

# Create an edge
task_id = akg.create_node("Task", {"title": "Fix Bug"})
akg.create_edge(user_id, task_id, "ASSIGNED_TO")

# Query
results = akg.query("MATCH (u:User)-[:ASSIGNED_TO]->(t:Task) RETURN t")
```

## Integration with LLMs

The `Joker Coordinator` exposes AKGS to LLMs via the MCP protocol. Models can "remember" context by writing to the graph and "recall" it by querying.
