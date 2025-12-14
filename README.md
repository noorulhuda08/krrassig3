# KRR Assignment 03 — Simple Multi-Agent Chat System

This is my Assignment 03 project for KRR. I made a small multi-agent chat system with a simple Gradio UI.  
It follows the lab/assignment idea: a Coordinator (manager) routes the work to other agents and we keep memory.

## What I built (4 agents)
- **Coordinator (Manager):** takes the user query, makes a small plan, calls other agents, and returns the final answer.
- **ResearchAgent:** does “mock web search” using a preloaded JSON knowledge base (`data/mock_web_kb.json`).
- **AnalysisAgent:** does simple reasoning like compare / summarize based on retrieved results.
- **MemoryAgent:** stores conversation + learned answers + agent status, and supports keyword + vector similarity search.

## How it works (simple flow)
1) User types a query in the UI  
2) Coordinator decides a plan (Research / Research+Analysis / Memory)  
3) ResearchAgent retrieves relevant items from the mock KB  
4) AnalysisAgent (if needed) produces a short summary/comparison  
5) Coordinator returns the answer and stores it into MemoryAgent for reuse

## About the mock knowledge base (my process)
Initially I created the mock KB using Australia-related facts (cities, landmarks, etc.) just to test that the pipeline and UI were working properly end-to-end. After that was stable, I added ML-related entries (neural networks, transformers, RL, comparisons) so the required assignment scenarios give meaningful answers.

## Folder structure
- `agents/` → agent code
- `data/mock_web_kb.json` → mock “web” database
- `tests/run_scenarios.py` → runs the 5 scenarios and saves logs
- `outputs/` → required output text files
- `storage/` → saved conversation + knowledge + agent state (auto created)

## How to run (local)
### 1) Install requirements
Activate your venv then:
pip install -r requirements.txt

### 2) Run UI
python app_gradio.py  
Open the link shown (usually): http://127.0.0.1:7860

### 3) Run the 5 assignment scenarios (creates outputs/)
python .\tests\run_scenarios.py

After running, check `outputs/` folder. It should contain:
- simple_query.txt
- complex_query.txt
- memory_test.txt
- multi_step.txt
- collaborative.txt

## Memory system (what I did)
- Conversation memory: `storage/conversation.jsonl`
- Knowledge base: `storage/knowledge.json`
- Agent state: `storage/agent_state.json`
- Retrieval:
  - keyword/topic matching
  - TF-IDF vector similarity (simple vector store approach)

This helps avoid repeating work because the Coordinator can reuse similar past answers.

## Docker (deliverable files)
I included Docker files (`Dockerfile` and `docker-compose.yaml`).  
To actually run Docker you need Docker installed on the machine.

Commands:
docker compose up --build  
Open: http://localhost:7860

## Notes / limitations
- “Web search” is simulated using the JSON KB (no real internet).
- Analysis is intentionally simple (compare/summarize) to keep the system lightweight and reproducible.

## AUTHOR
- Ali Rabeet Haider 231174
- Noor Ul Huda 231140
