# mcp-lite
The library for local work with AI tools without running MCP server.

### Installation

```python 
uv add mcp-lite
```

### Import

```python 
from mcp_lite import MCP
```

### Usage

```python
from typing import List

from mcp_lite import MCP, Tool


mcp = MCP()


@mcp.tool
def sync_add(a, b):
    """
    Call this function if you need to add two numbers.

    Args:
        a (int | float): The first number.
        b (int | float): The second number.
    """
    return a + b


@mcp.tool
async def async_mul(a, b):
    """
    Call this function if you need to multiply two numbers.

    Args:
        a (int | float): The first number.
        b (int | float): The second number.
    """
    return a * b


tools: List[Tool] = mcp.list_tools()

tools_description = "\n".join(
    f"- {tool.name}: {tool.description}" 
    for tool in tools
)

# Some code where AI calls some tools :)

for tool_call in tool_calls:
    tool_name = tool_call.get("tool_name")
    tool_args = tool_call.get("args", {})

    tool_result = await mcp.call_tool(tool_name, tool_args)

```
