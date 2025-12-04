# 🎬 Custom LLM Tools for a YouTube Agent (LangChain + Tool Calling)

This project implements a **YouTube-aware LLM agent** using **LangChain** and **custom tools**.  
The agent can:

- Extract YouTube video IDs from URLs  
- Fetch transcripts  
- Search YouTube by query  
- Retrieve rich video metadata  
- Fetch thumbnails  
- Orchestrate multi-step tool calls to produce final summaries or answers  

Everything is built using **LangChain tools + Runnable pipelines**, with OpenAI-style tool calling via `langchain-openai`.

---

## 🚀 What This Project Demonstrates

### 1. Building Custom Tools for LLMs

The notebook defines several tools using the `@tool` decorator:

- `extract_video_id(url: str)`  
- `fetch_transcript(video_id: str, language: str = "en")`  
- `search_youtube(query: str)`  
- `get_full_metadata(url: str)`  
- `get_thumbnails(url: str)`  

Each tool:

- Has a clear purpose and docstring  
- Uses an external library (`pytube`, `yt-dlp`, `youtube-transcript-api`)  
- Returns structured data that the LLM can reason over  

This shows how to **wrap real-world capabilities** behind tool interfaces the LLM can call.

---

### 2. OpenAI-Style Tool Calling with LangChain

Using:

- `llm = init_chat_model("gpt-4o-mini", model_provider="openai")`  
- `llm_with_tools = llm.bind_tools(tools)`  

The LLM:

- Receives a user query (e.g., “Summarize this YouTube video: <URL>”)  
- Decides which tool(s) to call (e.g., `extract_video_id` → `fetch_transcript`)  
- Calls them with structured arguments  
- Uses tool outputs to generate a final answer  

This demonstrates **tool-calling orchestration**, which is directly relevant to agentic AI systems.

---

### 3. Runnable Pipelines for Multi-Step Logic

The project builds higher-level chains using **LangChain Runnables**, such as:

- `summarization_chain`  
- `universal_chain`  
- Recursive tool processing with `RunnableLambda`  

These chains:

- Start from a single user query  
- Let the LLM request tools  
- Execute tools and append `ToolMessage` objects  
- Feed the updated message history back to the LLM  
- Repeat until no further tools are requested  
- Return the final response (e.g., a video summary or a list of trending videos)

This shows that tools are not just “one-off calls”, but can be part of **multi-step, iterative reasoning loops**.

---

### 4. Real YouTube Use Cases

Example capabilities:

- **Summarize a specific YouTube video**  
- **Get top matching videos for a query and inspect metadata**  
- **Retrieve and inspect thumbnail variants**  
- **Build a more general “universal_chain” that can handle flexible YouTube-related questions**

The project is intentionally designed to look like a **real-world backend component** of a YouTube research assistant or content analysis tool.

---

## 📂 Repository Structure

    custom-llm-tools-youtube-agent/
    ├── custom_llm_tools_youtube_agent.ipynb   # Main notebook
    ├── README.md                              # Project documentation
    ├── requirements.txt                       # Python dependencies
    ├── .gitignore                             # Git ignore rules
    └── LICENSE                                # MIT License

---

## 🛠️ Tech Stack

- **LangChain** – tools, messages, runnables  
- **langchain-openai** – OpenAI-style chat model integration  
- **pytube** – searching and basic video info  
- **youtube-transcript-api** – video transcripts  
- **yt-dlp** – rich video metadata and thumbnails  
- **Python 3.10+**  
- **Google Colab / Jupyter Notebook**  

---

## ▶️ How to Run

1. Clone the repository:

       git clone https://github.com/<your-username>/custom-llm-tools-youtube-agent.git
       cd custom-llm-tools-youtube-agent

2. Open the notebook `custom_llm_tools_youtube_agent.ipynb` in **Google Colab** or Jupyter.

3. Set your OpenAI API key in the environment (for example, in Colab):

       import os
       os.environ["OPENAI_API_KEY"] = "YOUR_API_KEY_HERE"

4. Run the installation cell.

5. Execute the cells step-by-step to:

   - Inspect the tools and their schemas  
   - Watch the LLM select tools  
   - See the message history evolve with `HumanMessage`, AI responses, and `ToolMessage` outputs  
   - Generate YouTube video summaries and metadata-driven answers  

---

## 📘 Key Learnings

This project demonstrates:

- How to design and implement **custom tools** for LLMs  
- How to integrate **external APIs and libraries** into an LLM workflow  
- How to use **tool-calling** and **multi-step chains** for non-trivial tasks  
- How to structure a YouTube-focused agent that feels production-oriented  

---

## 📄 License

This project is released under the **MIT License**.

---

## 💬 Author

**Kavitha Lingarajegowda**  
Agentic AI Engineering | LLM Systems | YouTube AI Tools  
LinkedIn | Portfolio
