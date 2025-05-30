
# 📘 README: Autonomous Agent-Orchestrated Story Creation Pipeline

## Overview

This project showcases a coordinated agent system that autonomously generates a children's book titled *"Tim the Flying Dog"*. It leverages a **multi-agent orchestration model** using **OpenAI language models**, facilitated through a central "Editor Agent". The entire pipeline is encapsulated in a cleanly modular architecture using asynchronous Python constructs.

The system is designed to emulate a publishing workflow: from plotting, to drafting, critique, and final editing—mirroring a simplified human editorial process.

---

## Architecture Summary

### Agent Roles

* **Plot Agent** – Crafts a child-appropriate plot outline.
* **Writer Agent** – Develops a whimsical narrative from the plot.
* **Critic Agent** – Provides constructive literary critique.
* **Editor Agent** – Orchestrates the end-to-end workflow by invoking other agents as tools.

Each agent uses consistent **language model settings** to ensure coherent style and predictable behavior across phases.

---

## Key Features

* 🔁 Multi-agent coordination with logical handoffs
* 🤖 GPT-based creativity with structured instruction templates
* 📡 SSE-compatible agent server (via `MCPServerSse`, although unused here)
* 🧪 Execution tracing and structured output formatting
* 🚸 Child-centric narrative targeting ages 5–8

---

## Prerequisites

Ensure the following before execution:

* Python ≥ 3.8
* OpenAI API key:

  ```bash
  export OPENAI_API_KEY='your-api-key'
  ```

---

## Dependencies

* `agents`: Local module containing the agent orchestration utilities (`Agent`, `Runner`, `trace`, etc.)
* `asyncio`: Enables non-blocking agent invocation
* `os`: Used to fetch environmental configuration
* `dataclasses` (implied): For structured agent/tool definitions

---

## Agent Definitions

### `plot_agent`

* **Purpose**: Outputs a structured plot.
* **Tone**: Child-friendly, imaginative, light conflict and resolution.

### `writer_agent`

* **Purpose**: Converts the plot into a full story.
* **Constraints**: Use simple, whimsical language and vivid imagery.

### `critic_agent`

* **Purpose**: Suggests improvements in tone, clarity, pacing, and engagement.
* **Note**: Does not rewrite the story—only critiques.

### `editor_agent`

* **Purpose**: Central orchestration unit using above agents as callable tools.

* **Behavior**:

  1. Requests a plot.
  2. Passes plot to the writer.
  3. Passes draft to the critic.
  4. Sends critique back to writer.
  5. Outputs final version.

* **Output Format**: Responses follow the schema `{stage: ..., content: ...}` to ensure interpretability.

---

## Execution Flow

The script's entry point is `run_book_creation()`, which does the following:

1. Sends a coordination prompt to the **Editor Agent**.
2. Triggers internal tool usage in sequence (Plot → Writer → Critic → Writer).
3. Prints out trace logs per agent step:

   ```plaintext
   🔧 Agent: Writer Agent
   ➡️ Input: ...
   ✅ Output: ...
   ```
4. Displays the final story:

   ```plaintext
   ✅ Final Book Output:
   ...
   ```

---

## Example Usage

```bash
python story_pipeline.py
```

Expected Output:

```
>> Running Editor Agent with input: Please coordinate the book creation process for 'Tim the Flying Dog'.

🔧 Agent: Plot Agent
➡️ Input: ...
✅ Output: ...

...

✅ Final Book Output:
<Final revised children's story>
```

---

## Extensibility

You can expand this framework by:

* Introducing **additional tools** (e.g., Illustrator Agent, Title Agent).
* Parameterizing agent prompts for different story genres or age groups.
* Wrapping the pipeline in a **web server** using FastAPI for interactive usage.
* Adding **SSE output streaming** via the included `MCPServerSse`.

---

## File Structure

```
.
├── story_pipeline.py               # Main execution script
├── agents/
│   ├── __init__.py
│   ├── Agent.py
│   ├── Runner.py
│   ├── mcp.py                      # Optional: for SSE server
│   └── model_settings.py
└── README.md
```

---

## License

This project is distributed for educational and research purposes. Ensure compliance with the OpenAI API usage terms.

---

## Author

**John Williams**
Professor of Physics and IT
GeoSpatial

