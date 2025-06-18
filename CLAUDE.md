# MCP Demo Instructions for Claude Code

## Context Files
- `@context/llms-full.txt` - Contains MCP documentation and client information
- `@talk/index.html` - Your presentation slides

## Live Demo Plan

When asked to create a simple MCP server demo, follow these steps:

1. **Create project structure**:
   ```
   demo_mcp_server/
   ├── pyproject.toml
   ├── server.py
   └── README.md
   ```

2. **Implement the MCP server** with:
   - At least one resource
   - At least one tool
   - Clear, fun functionality
   - Error handling
   - Good documentation

3. **Show configuration** for Claude Desktop:
   ```json
   {
     "mcpServers": {
       "demo-server": {
         "command": "python",
         "args": ["path/to/server.py"]
       }
     }
   }
   ```

4. **Test the server** by running it locally

## Important Commands
- Install MCP: `pip install mcp`
- Run server: `python server.py`
- Test with stdio: `python server.py` (then type JSON-RPC commands)

## Best Practices for Demo
- Keep it simple but impressive
- Show real-time functionality
- Include helpful error messages
- Make it interactive and fun
- Show both resources AND tools