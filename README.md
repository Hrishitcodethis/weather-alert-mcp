# MCP Weather Agent

This project demonstrates an AI agent (MCPAgent) that uses the MCPClient to interact with a weather tool to provide weather alerts.

## Setup

Follow these steps to set up and run the project:

1.  **Clone the Repository:**
    ```bash
    git clone https://github.com/Hrishitcodethis/weather-alert-mcp.git # Replace with actual repo URL
    cd weather-alert-mcp
    ```

2.  **Set up Environment Variables:**
    Create a `.env` file in the root directory of the project based on `.env.example`.
    ```
    OPENAI_API_KEY="YOUR_OPENAI_API_KEY"
    ```
    Replace `"YOUR_OPENAI_API_KEY"` with your actual OpenAI API key.

3.  **Install Dependencies:**
    It is recommended to use `uv` for dependency management. If you don't have `uv` installed, you can install it via pip:
    ```bash
    pip install uv
    ```
    Then, install the project dependencies:
    ```bash
    uv pip install -r requirements.txt
    ```
    *(Note: You might need to create a `requirements.txt` file based on your `pyproject.toml` or manually add dependencies if not already present.)*

4.  **Start Docker Containers:**
    Ensure Docker Desktop is running. This project utilizes Docker for some services (e.g., the weather tool).
    ```bash
    docker-compose up -d
    ```
    *(Note: A `docker-compose.yml` file is assumed to be present for this step.)*

## Usage

To run the interactive chat with the MCP Weather Agent:

```bash
python server/client.py
```

Once the chat starts, you can type your queries related to weather alerts.

## Workflow

The `MCPAgent` in `server/client.py` is configured to use `MCPClient` which connects to the `weather.json` configuration. The `weather.json` file defines how the `mcp_weather_get_alerts` tool is exposed to the agent.

1.  **User Input:** The `client.py` script takes user input.
2.  **Agent Processing:** The `MCPAgent` processes the user's query.
3.  **Tool Calling:** If the query is related to weather alerts, the agent identifies and calls the `mcp_weather_get_alerts` tool via the `MCPClient`.
4.  **Tool Execution:** The `MCPClient` executes the `mcp_weather_get_alerts` function, which fetches weather alerts for the specified state.
5.  **Response Generation:** The agent receives the result from the tool and generates a human-readable response using the `ChatOpenAI` model.
6.  **Conversation Memory:** The agent maintains conversation memory, allowing for context-aware interactions.

The `run_memory_chat` function in `server/client.py` orchestrates this interactive chat experience.
