8# Deep Research Agent

<img width="1388" height="298" alt="full_diagram" src="https://github.com/user-attachments/assets/12a2371b-8be2-4219-9b48-90503eb43c69" />



###  Quickstart

1. Clone the repository and activate a virtual environment:
```bash
git clone https://github.com/langchain-ai/open_deep_research.git
cd open_deep_research
uv venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate
```

2. Install dependencies:
```bash
uv pip install -r pyproject.toml
```

3. Set up your `.env` file to customize the environment variables (for model selection, search tools, and other configuration settings):
```bash
cp .env.example .env
```

4. Launch the assistant with the LangGraph server locally to open LangGraph Studio in your browser:

```bash
# Install dependencies and start the LangGraph server
uvx --refresh --from "langgraph-cli[inmem]" --with-editable . --python 3.11 langgraph dev --allow-blocking
```

Use this to open the Studio UI:
```
-  API: http://127.0.0.1:2024
-  Studio UI: https://smith.langchain.com/studio/?baseUrl=http://127.0.0.1:2024
-  API Docs: http://127.0.0.1:2024/docs
```
<img width="817" height="666" alt="Screenshot 2025-07-13 at 11 21 12 PM" src="https://github.com/user-attachments/assets/052f2ed3-c664-4a4f-8ec2-074349dcaa3f" />

Ask a question in the `messages` input field and click `Submit`.

### Configurations


#### General Settings

- **Max Structured Output Retries** (default: 3)
- **Allow Clarification** (default: true)
- **Max Concurrent Research Units** (default: 5)

#### Research Configuration

- **Search API** (default: Tavily)
- **Max Researcher Iterations** (default: 3)
- **Max React Tool Calls** (default: 5)

#### Models

Open Deep Research uses multiple specialized models for different research tasks:

- **Summarization Model** (default: `openai:gpt-4.1-nano`): Summarizes research results from search APIs
- **Research Model** (default: `openai:gpt-4.1`): Conducts research and analysis 
- **Compression Model** (default: `openai:gpt-4.1-mini`): Compresses research findings from sub-agents
- **Final Report Model** (default: `openai:gpt-4.1`): Writes the final comprehensive report




#### Local MCP Servers

**Filesystem MCP Server** provides secure file system operations with robust access control:
- Read, write, and manage files and directories
- Perform operations like reading file contents, creating directories, moving files, and searching
- Restrict operations to predefined directories for security
- Support for both command-line configuration and dynamic MCP roots

Example usage:
```bash
mcp-server-filesystem /path/to/allowed/dir1 /path/to/allowed/dir2
```

#### Remote MCP Servers  

**Remote MCP servers** enable distributed agent coordination and support streamable HTTP requests. Unlike local servers, they can be multi-tenant and require more complex authentication.

**Arcade MCP Server Example**:
```json
{
  "url": "https://api.arcade.dev/v1/mcps/ms_0ujssxh0cECutqzMgbtXSGnjorm",
  "tools": ["Search_SearchHotels", "Search_SearchOneWayFlights", "Search_SearchRoundtripFlights"]
}
```

Remote servers can be configured as authenticated or unauthenticated and support JWT-based authentication through OAuth endpoints.

### Evaluation

A comprehensive batch evaluation system designed for detailed analysis and comparative studies.

#### **Features:**
- **Multi-dimensional Scoring**: Specialized evaluators with 0-1 scale ratings
- **Dataset-driven Evaluation**: Batch processing across multiple test cases

#### **Usage:**
```bash
# Run comprehensive evaluation on LangSmith datasets
python tests/run_evaluate.py
```
#### **Key Files:**
- `tests/run_evaluate.py`: Main evaluation script
- `tests/evaluators.py`: Specialized evaluator functions
- `tests/prompts.py`: Evaluation prompts for each dimension

