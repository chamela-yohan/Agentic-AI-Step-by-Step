# LangGraph Tutorial Notebook

This notebook provides a comprehensive tutorial on building agentic workflows using LangGraph, covering basic graph structures, integration with Large Language Models (LLMs), tool usage, and Retrieval Augmented Generation (RAG).

## Table of Contents

1.  [Stage 1: Simple Graph](#stage-1-simple-graph)
2.  [Stage 2: With LLM](#stage-2-with-llm)
3.  [Stage 3: Agent + Use Tools](#stage-3-agent--use-tools)
4.  [Stage 4: Agent with RAG](#stage-4-agent-with-rag)

## Stage 1: Simple Graph

This section introduces the fundamental concepts of LangGraph, demonstrating how to create and compile a `StateGraph` with nodes and edges.

### Key Concepts:

*   **`TypedDict`**: Used to define the state schema (`AgentState`).
*   **Nodes**: Functions that represent steps in the workflow (e.g., `hello_name`, `hello_age`).
*   **Edges**: Define the transitions between nodes, including `START` and `END` points.
*   **Conditional Edges**: Illustrated with an arithmetic example (`addition`, `substract`, `multiply`, `divide`) and a `decision_node` to route based on the operation.

### Libraries Used:

*   `langgraph.graph.StateGraph`
*   `langgraph.graph.START`, `langgraph.graph.END`
*   `IPython.display.Image`

## Stage 2: With LLM

This section focuses on integrating a Large Language Model (LLM) into a LangGraph workflow using Google's Gemini API.

### Key Concepts:

*   **LLM Integration**: Demonstrates how to use `ChatGoogleGenerativeAI` within a node to generate responses.
*   **API Key Management**: Securely loading API keys using `google.colab.userdata`.
*   **Agent State for Messages**: Managing conversational history with `HumanMessage` and `AIMessage`.

### Libraries Used:

*   `langchain_google_genai.ChatGoogleGenerativeAI`
*   `langchain_core.messages.HumanMessage`, `langchain_core.messages.AIMessage`

## Stage 3: Agent + Use Tools

This stage enhances the LLM-powered agent by enabling it to use external tools for more complex tasks, such as calculations.

### Key Concepts:

*   **Tools**: Defining functions as tools using the `@tool` decorator (e.g., `addition`, `subtraction`, `multiplication`, `devision`).
*   **Tool Binding**: Binding tools to the LLM using `llm.bind_tools()`.
*   **ToolNode**: A LangGraph component for executing tool calls made by the LLM.
*   **Conditional Routing**: The `decision_node` checks for `tool_calls` in the LLM's response to decide whether to execute a tool or end the interaction.

### Libraries Used:

*   `langchain_core.tools.tool`
*   `langgraph.prebuilt.ToolNode`

## Stage 4: Agent with RAG

This section demonstrates how to build a Retrieval Augmented Generation (RAG) system within LangGraph, allowing the agent to retrieve information from a document to answer questions.

### Key Concepts:

*   **Document Loading**: Using `PyPDFLoader` to load PDF documents.
*   **Text Splitting**: Employing `RecursiveCharacterTextSplitter` to break down documents into manageable chunks.
*   **Embeddings**: Generating vector embeddings for document chunks using `GoogleGenerativeAIEmbeddings`.
*   **Vector Store**: Storing and indexing document embeddings using `Chroma`.
*   **Retriever**: Creating a retriever to fetch relevant document chunks based on a query.
*   **`retriever_tool`**: A custom tool that encapsulates the retrieval logic.
*   **RAG Workflow**: Integrating the `retriever_tool` into the LangGraph workflow, enabling the LLM to use retrieved information to answer questions about the provided PDF document.
*   **System Prompt**: Guiding the AI assistant to use the retriever tool and cite sources.

### Libraries Used:

*   `chromadb`
*   `langchain-chroma`
*   `langchain_community.document_loaders.PyPDFLoader`
*   `langchain_text_splitters.RecursiveCharacterTextSplitter`
*   `langchain_google_genai.GoogleGenerativeAIEmbeddings`
