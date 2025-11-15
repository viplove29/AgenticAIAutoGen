# AgenticAI AutoGen Framework

## Overview

AgenticAI AutoGen is a comprehensive framework for building multi-agent AI systems using Microsoft's AutoGen library. The framework provides a factory pattern for creating specialized agents that can collaborate on complex tasks using Model Context Protocol (MCP) integrations.

## Project Structure

```
AgenticAIAutoGen/
├── framework/
│   ├── agentFactory.py       # Factory for creating specialized agents
│   ├── mcp_config.py         # MCP server configurations
│   ├── scenario2.py          # Multi-agent registration workflow
│   └── __init__.py
├── basics1.py through basics6.py  # Foundational examples
├── scenario1.py              # Bug analysis & automation scenario
├── selectorGroup.py          # Research & writing workflow
├── web_surfer.py             # Web browsing agent
└── memory.json               # Agent state persistence
```

## Framework Components

#### agentFactory.py

Factory class that creates pre-configured agents with integrated MCP workbenches:

- **`create_database_agent()`** - MySQL database agent with query capabilities
- **`create_api_agent()`** - REST API agent with filesystem access
- **`create_excel_agent()`** - Excel file management agent

#### mcp_config.py

Centralized configuration for Model Context Protocol servers:

- **MySQL Workbench** - Database operations (host: localhost:3306, db: rahulshettyacademy)
- **REST API Workbench** - HTTP requests (base: https://rahulshettyacademy.com)
- **Excel Workbench** - Spreadsheet operations
- **Filesystem Workbench** - File system access

#### scenario2.py

**Sequential User Registration Workflow** - Demonstrates multi-agent collaboration:

- **DatabaseAgent** - Retrieves registration data from MySQL tables
- **APIAgent** - Executes registration and login API calls with validation
- **ExcelAgent** - Persists successful registrations to Excel files

**Key Features:**

- Structured data passing between agents
- API response validation
- Conditional Excel writes (only on successful login)
- Round-robin team coordination with text-based termination

## Core Examples

| File             | Purpose                      | Key Feature                            |
| ---------------- | ---------------------------- | -------------------------------------- |
| basics1.py       | Simple single agent          | Basic OpenAI integration               |
| basics2.py       | Agent conversation           | Two-agent dialogue                     |
| basics3.py       | Multi-agent team             | Math tutor conversation                |
| basics4.py       | User proxy interaction       | Human-in-the-loop agent                |
| basics5.py       | State persistence            | Agent memory with JSON                 |
| basics6.py       | Filesystem access            | MCP filesystem tools                   |
| scenario1.py     | Jira + Playwright automation | Bug analysis & automated testing       |
| selectorGroup.py | Dynamic agent selection      | Research → Writing → Critique workflow |
| web_surfer.py    | Web browsing                 | Multimodal web interaction             |

## Getting Started

### Prerequisites

```bash
pip install autogen-agentchat autogen-ext[openai]
```

### Environment Variables

```bash
export OPENAI_API_KEY="your-api-key"
export MYSQL_HOST="localhost"
export MYSQL_PORT="3306"
export MYSQL_USER="root"
export MYSQL_PASSWORD="root1234"
export MYSQL_DATABASE="rahulshettyacademy"
```

### Running an Example

```bash
# Simple agent task
python basics1.py

# Multi-agent workflow
python framework/scenario2.py

# Bug analysis & automation
python scenario1.py
```

## Key Concepts

### Agent Types

- **AssistantAgent** - LLM-powered agent with system messages
- **UserProxyAgent** - Human user representation in multi-agent teams
- **MultimodalWebSurfer** - Web navigation and visual analysis

### Team Coordination

- **RoundRobinGroupChat** - Sequential agent turns
- **SelectorGroupChat** - AI-selected next agent
- **Termination Conditions** - TextMentionTermination, MaxMessageTermination

### MCP Integration

Agents access external tools through Model Context Protocol:

- Database queries
- REST API calls
- File operations
- Excel manipulation
- Web browsing

## Advanced Features

✅ **Agent State Persistence** - Save and load agent memory via JSON  
✅ **Multi-workbench Support** - Single agent with multiple MCP integrations  
✅ **Conditional Workflows** - Agents make decisions based on peer outputs  
✅ **Structured Data Passing** - Clear handoff formats between agents  
✅ **Async/Await Pattern** - Non-blocking concurrent agent execution

## Common Patterns

### Sequential Workflow

```python
# Agent A completes → Agent B starts → Agent C completes
RoundRobinGroupChat(participants=[agent_a, agent_b, agent_c])
```

### Conditional Handoff

```python
# Agent A writes: "TASK_COMPLETE" → Triggers Agent B
TextMentionTermination("TASK_COMPLETE")
```

### State Management

```python
state = await agent.save_state()
# ... persist/restore ...
await agent.load_state(state)
```

## Supporting Files & Utilities

### memory.json

- **Purpose**: Persistent agent state storage
- **Usage**: Agents save conversation history, memory, and configuration
- **Format**: JSON structure for easy serialization and debugging

### algebra_explanation.txt

- **Purpose**: Sample output demonstrating agent math tutoring capability
- **Content**: Markdown-formatted algebra problem explanations
- **Use Case**: Example of agent-generated educational content

## Notes

- API keys are embedded in examples - use environment variables in production
- MySQL paths assume Mac installation; adjust for your OS
- Excel operations require valid file paths
- All examples are async and require Python 3.8+

## Documentation

This project includes comprehensive documentation:

- **Main README** (`README.md`) - Overview and getting started guide
- **Framework README** (`framework/README.md`) - Detailed framework API and configuration documentation
- **Code Examples** (`basics1.py` - `basics6.py`) - Foundational patterns and concepts
- **Scenario Workflows** (`scenario1.py`, `scenario2.py`, `selectorGroup.py`) - Complete end-to-end examples

## Directory Organization

- **`framework/`** - Core framework code with factory pattern and MCP configurations
- **`basics*.py`** - Step-by-step learning examples (basics1 through basics6)
- **`scenario*.py`** - Complex multi-agent workflows and automation examples
- **`web_surfer.py`** - Specialized web browsing agent example
- **`memory.json`** - Sample agent state persistence file
- **`algebra_explanation.txt`** - Sample agent output for educational tasks

## Resources

- [AutoGen Documentation](https://microsoft.github.io/autogen/)
- [Model Context Protocol](https://modelcontextprotocol.io/)
- [OpenAI API Reference](https://platform.openai.com/docs/api-reference)
