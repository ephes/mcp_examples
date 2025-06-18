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
   
   Note: Edit config with `code ~/Library/Application\ Support/Claude/claude_desktop_config.json`

4. **Test the server** by running it locally

## Important Commands
- Install MCP: `pip install mcp` or with uv: `/Users/jochen/.cargo/bin/uv add mcp`
- Run server: `python server.py`
- Test with stdio: `python server.py` (then type JSON-RPC commands)

## MCP SDK Changes - IMPORTANT
The MCP SDK has evolved significantly. Key changes:
1. **Use FastMCP instead of low-level Server**: The new SDK uses `from mcp.server.fastmcp import FastMCP`
2. **Decorators for resources and tools**: Use `@mcp.resource()` and `@mcp.tool()` decorators
3. **Simplified initialization**: Just call `mcp.run()` in the main block
4. **No async/await needed**: FastMCP handles async operations internally for simple cases
5. **Resources use URI patterns**: Resources can have dynamic URIs like `"resource://{param}"`

## Using uv for MCP Servers
- Use full path to uv: `/Users/jochen/.cargo/bin/uv`
- Create venv: `/Users/jochen/.cargo/bin/uv venv -p python3.13.4`
- Install dependencies: `/Users/jochen/.cargo/bin/uv sync`
- Run server with uv: `/Users/jochen/.cargo/bin/uv run python server.py`
- Claude Desktop config should use full uv path:
  ```json
  {
    "command": "/Users/jochen/.cargo/bin/uv",
    "args": ["run", "python", "/full/path/to/server.py"]
  }
  ```

## Important pyproject.toml Configuration
- Use `mcp[cli]` instead of just `mcp` for the dependency
- Use uv_build as the build backend:
  ```toml
  [build-system]
  requires = ["uv_build>=0.7.8,<0.8.0"]
  build-backend = "uv_build"
  ```
- Requires Python >=3.10 (MCP doesn't support Python 3.9)

## Package Structure Requirements
- When using `uv_build`, you MUST use proper Python package structure:
  ```
  project_name/
  ├── pyproject.toml
  ├── src/
  │   └── package_name/
  │       ├── __init__.py
  │       └── server.py
  └── README.md
  ```
- The package must be in `src/package_name/` directory
- Include an `__init__.py` file in the package directory

## Claude Desktop Configuration with uv
- **IMPORTANT**: Use `--directory` flag with `uv` to specify the project directory
- Run as a Python module using `-m` flag
- Correct configuration format:
  ```json
  {
    "mcpServers": {
      "server-name": {
        "command": "/Users/jochen/.cargo/bin/uv",
        "args": [
          "--directory",
          "/path/to/project",
          "run",
          "python",
          "-m",
          "package_name.server"
        ]
      }
    }
  }
  ```
- The module path follows Python import syntax: `package_name.server` for `src/package_name/server.py`
- This ensures uv runs in the correct environment with all dependencies available

## Best Practices for Demo
- Keep it simple but impressive
- Show real-time functionality
- Include helpful error messages
- Make it interactive and fun
- Show both resources AND tools