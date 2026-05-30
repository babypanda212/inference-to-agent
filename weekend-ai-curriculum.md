# Weekend Hackathon Curriculum: From One Inference Call to a Local Agent

**For:** Ayesha
**Format:** Weekend hackathon. Time-boxed, build-driven, ship something by Sunday night.
**Created:** 2026-05-30
**Covers:** the gap between "classical-ML inference" and "using the Claude app" - web fundamentals, the LLM stack, agents, RAG, local-first.

---

## The one idea this weekend teaches

There is a stack. You have only ever touched the top and (in classical ML) the bottom. This weekend you walk the whole thing and build your own version of the middle.

```
TOP     Claude Desktop app / Pi        <- a HARNESS (loop + tools + memory). You live here.
         │
MIDDLE  the loop, tools, RAG, prompting <- you have NEVER been here. This is the weekend.
         │
BOTTOM  one LLM inference call          <- you have never made one (classical-ML inference yes, LLM no).
```

By Sunday night you will have hand-built a tiny harness yourself. After that, "what is Pi," "what is the Claude app," and "what does it mean to build an agent" are no longer abstract - you will have seen the inside.

## Rules of the hackathon

1. **Build over read.** Every block ends in a script that runs, not notes. Read only as far as the next build step needs.
2. **Local-first.** Everything runs on Ollama on your Mac. No cloud API keys. This is the environmental point made real.
3. **Right-size on purpose.** Start with the smallest model that works. Feel the speed/quality tradeoff yourself. That instinct is the whole environmental argument: route each task to the lightest sufficient tool.
4. **Log as you go.** One line per block: what you built, what surprised you. (Your standing preference: decisions logged, not just in your head.)
5. **freeCodeCamp + local docs only.** No Anthropic resources by your rule. Pi specifics from pi.dev (not Anthropic).

## What you ship by Sunday night (the capstone)

**"Ask-my-folder": a fully-local document-Q&A agent.** Point it at a folder of documents. Ask a question. It retrieves the relevant pieces (RAG), reasons over them with tools in a loop, and answers - grounded in your files, running entirely on your laptop. This single project exercises every layer: inference call -> calling from code -> prompting -> structured output -> tool use -> the loop -> RAG -> local serving. It is also a cousin of your content-intelligence tool's evidence-trail idea (grounding answers in real content).

---

## Block 0 - Friday evening (~1.5 hrs): First contact

**Goal:** working environment + your first LLM inference call, fully local.

**Do:**
- Confirm Ollama is installed; pull a small model (`ollama pull llama3.1:8b` or `qwen2.5`). You already run Qwen 14B for the hackathon, so this may be quick.
- Run the freeCodeCamp Python script that calls the local model at `http://localhost:11434`.

**Resource:** [How To Run an Open-Source LLM on Your Personal Computer: Run Ollama Locally](https://www.freecodecamp.org/news/how-to-run-an-open-source-llm-on-your-personal-computer-run-ollama-locally/)

**Deliverable:** `00_first_call.py` - a script that prints a model's answer to a prompt you wrote. This is your first LLM inference call.

**Why it matters:** This is the bottom of the stack the Claude app has been hiding from you. Once you have done it once, the mystique is gone.

---

## Block 1 - Saturday morning (~3 hrs): The wire underneath

**Goal:** see that an "LLM call" is just an HTTP request, and that you can talk to any model the same way. This is also your HTTP / REST / API fundamentals, learned in context.

**Do:**
- Skim the concepts: requests, responses, endpoints, JSON, status codes.
- Call your local model **three ways**: the native `ollama` library, an OpenAI-compatible SDK pointed at Ollama, and raw `requests` to the endpoint. Print the raw request and response each time.

**Resources:**
- [APIs for Beginners](https://www.freecodecamp.org/news/apis-for-beginners/) (concepts, skim)
- [Python Requests: Interact with Web Services](https://www.freecodecamp.org/news/how-to-interact-with-web-services-using-python/)
- [Protect Sensitive Data by Running LLMs Locally with Ollama](https://www.freecodecamp.org/news/protect-sensitive-data-with-local-llms/) (the 3-ways tutorial)

**Deliverable:** `01_three_ways.py` - same prompt, three client methods, and you can point to the HTTP request hiding inside each.

**Why it matters:** "Same model, three clients" is the provider-agnostic insight made concrete. It is exactly why a harness like Pi can swap models with a config change. Endpoints, request/response, and polling all live here - your web-fundamentals goal, paid off inside a real task.

---

## Block 2 - Saturday afternoon (~4 hrs): Structured output + your first tool

**Goal:** get reliable machine-usable output, and let the model call a function.

**Do:**
- Structured output: ask the model for JSON in a fixed shape; validate it in code; handle the case where it returns junk.
- Function calling: define ONE tool (e.g. a calculator, or `read_file(path)`). Let the model decide when to call it, run it in your code, feed the result back, get the final answer.

**Resources:**
- [How to Structure JSON Responses with Function Calling](https://www.freecodecamp.org/news/how-to-get-json-back-from-chatgpt-with-function-calling/)
- [How to Build Agentic AI Workflows](https://www.freecodecamp.org/news/how-to-build-agentic-ai-workflows/) (first half: system prompts, tools)

**Deliverable:** `02_one_tool.py` - the model answers a question it cannot answer alone by emitting a structured tool call that your code runs.

**Why it matters:** This is the atom of an agent: model + a tool it can invoke. Two of the three ingredients are now in your hands. It also echoes your hackathon's rule "code computes numbers, the model writes prose" - structured output is how you wall the model off from where it is unreliable.

---

## Block 3 - Sunday morning (~3.5 hrs): The loop = your first agent

**Goal:** turn the single tool call into a loop. This is a real (tiny) agent.

**Do:**
- Wrap call + tool in a `while` loop with a stopping condition.
- Give it two tools (e.g. `list_files`, `read_file`).
- Ask a question that needs several steps. Print each iteration so you watch it think -> act -> observe -> repeat.

**Resource:** [How to Build Agentic AI Workflows](https://www.freecodecamp.org/news/how-to-build-agentic-ai-workflows/) (second half: the loop, memory, Supervisor/Swarm patterns)

**Deliverable:** `03_agent.py` - an agent that answers a multi-step question by calling tools in a loop until done.

**Why it matters:** You have now hand-built a harness. The Claude app and Pi are *this*, scaled and polished. "What does it mean to build an agent" is now something you have done, not read.

---

## Block 4 - Sunday afternoon (~4 hrs): Grounding (RAG) + ship + reflect

**Goal:** make the agent answer from YOUR documents, fully local, and ship the capstone.

**Do:**
- Add retrieval: embed a folder of documents with `nomic-embed-text` via Ollama, store the vectors, retrieve the most relevant chunks for a question, feed them to the model as context.
- Combine with your Block 3 loop. That is "ask-my-folder."
- Write a half-page reflection: what each layer does, and where the Claude app / Pi sit on your stack diagram.

**Resource:** [Build Your Own Local AI: Free RAG and AI Agents with Qwen 3 and Ollama](https://www.freecodecamp.org/news/build-a-local-ai/)

**Deliverable:** `04_ask_my_folder.py` - a working local document-Q&A agent + a short write-up.

**Why it matters:** RAG is grounding - the same idea as the evidence trail in your content tool. You have now built the stack top to bottom and grounded it in real data, entirely on your own machine.

---

## After the weekend (optional, not part of the sprint)

- **Swap your hand-rolled loop for a real harness.** Wire the capstone through Pi ([pi.dev](https://pi.dev), `earendil-works/pi`) and route easy steps to the 8B local model, hard steps to a larger one. That is the right-sizing dial, live - the environmental lever as a config setting.
- **Go deeper:** [Learn Python and Build Autonomous Agents](https://www.freecodecamp.org/news/learn-python-and-build-autonomous-agents/) (6 hrs, includes FastAPI, which is also your hackathon backend); [Beginner's Guide to LangChain](https://www.freecodecamp.org/news/beginners-guide-to-langchain/); [How to Start Building Projects with LLMs](https://www.freecodecamp.org/news/how-to-start-building-projects-with-llms/).

## By Sunday night you will be able to

- Make an LLM inference call from your own code, locally, and explain the HTTP request underneath it.
- Get structured (JSON) output and let a model call a tool.
- Build the think -> act -> observe loop that turns a model into an agent.
- Ground a model in your own documents with RAG.
- Explain precisely how Pi and the Claude app differ from the Claude *model*, because you built a small version of what they are.
- Right-size: choose the lightest sufficient model for a task, on purpose.

## Resource index

| Block | Resource |
|---|---|
| 0 | [Run Ollama Locally (first LLM call)](https://www.freecodecamp.org/news/how-to-run-an-open-source-llm-on-your-personal-computer-run-ollama-locally/) |
| 1 | [APIs for Beginners](https://www.freecodecamp.org/news/apis-for-beginners/) · [Python Requests](https://www.freecodecamp.org/news/how-to-interact-with-web-services-using-python/) · [Local LLMs 3 ways](https://www.freecodecamp.org/news/protect-sensitive-data-with-local-llms/) |
| 2 | [JSON + Function Calling](https://www.freecodecamp.org/news/how-to-get-json-back-from-chatgpt-with-function-calling/) · [Agentic AI Workflows](https://www.freecodecamp.org/news/how-to-build-agentic-ai-workflows/) |
| 3 | [Agentic AI Workflows](https://www.freecodecamp.org/news/how-to-build-agentic-ai-workflows/) |
| 4 | [Local AI: RAG + Agents with Qwen3 + Ollama](https://www.freecodecamp.org/news/build-a-local-ai/) |
| Later | [Autonomous Agents (6hr)](https://www.freecodecamp.org/news/learn-python-and-build-autonomous-agents/) · [LangChain guide](https://www.freecodecamp.org/news/beginners-guide-to-langchain/) · [Projects with LLMs](https://www.freecodecamp.org/news/how-to-start-building-projects-with-llms/) · Pi: [pi.dev](https://pi.dev) |
