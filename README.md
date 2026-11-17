# Christian Bakhos

I build AI agents that take real actions, and the evaluations that show whether they are safe to deploy.

Most of my work is shipped for enterprise customers, so the code is private. The public project below shows how I work: frozen test sets, deterministic grading, and every number reproducible from the repo.

## Featured: [AccessFrontier](https://github.com/Christianb0011/access-frontier)

An agent harness and frozen benchmark for enterprise access (IAM) tickets, built in a hackathon on Fireworks AI.

**The problem.** An agent's reply can be correct while the action it executed was unsafe. In one recorded case, a frontier model granted payroll write access to a disabled user, revoked it, then replied "request refused". Answer-only evaluation scores that as a pass.

**What I built.** A 305-case held-out benchmark that grades the state change the agent executed, not just its reply: a deterministic simulator with 8 tools and 8 policies, built from real IT tickets. Policies are enforced at the tool boundary, so violating writes are blocked before they execute. I also built an agentic layer between the model and the tools that completes missing lookups and enforces a strict output contract.

**Results.**
- **Safety:** GLM-5.3 made 3 policy-violating writes on its own. Behind the guard it made 0, and its hard-set score rose from 81.9% to 96.2%.
- **Cost:** a model about 9× cheaper (GLM-5.3 Flash) plus the harness scored 99.0% on both held-out sets, at $4.19 vs $36.27 per 10,000 tickets.
- **What I report honestly:** on the lenient metric the top systems tie at 99.5%. Most of the cheap model's lift comes from enforcing an output contract that other systems can parse reliably. The README says so, along with a fine-tune I trained but couldn't evaluate.

Test sets, tools, policies, simulator and scorer are hash-locked before any run. A pre-commit hook blocks changes to them, train/test leakage and secrets. I made 47 of the 49 commits; my teammate built the independent eval harness and the guard design my agentic layer follows.

## Other work (private: client or company code, walkthroughs on request)

- **Multi-agent maintenance planner for railways.** Six agents (orchestrator, asset history, spare parts, inventory, technicians, workshop slots) coordinate over the A2A protocol to produce maintenance proposals, with live progress streaming. Microsoft Agent Framework, FastAPI, Vue.
- **Claims-processing agent for a logistics company.** Reads monthly dispute files, applies business rules, checks parcel photos with a vision model, and recommends credit, no credit or review for each parcel. An analyst makes the final call.
- **Multilingual voice and text assistant for a science podcast.** Answers in Dutch, English or French with citations that link to episode timestamps. A Durable Functions pipeline transcribes and indexes new episodes. React 19, FastAPI, Azure AI Foundry, Voice Live, AI Search.
- **Voice-to-voice 3D avatar** for visitors at an innovation centre. Azure OpenAI Realtime API, lip sync, selectable personas, webcam-based visitor greeting.
- **Conservation kiosk with AI rhino identification** for a South African non-profit. Vue 3 on Azure Static Web Apps.
- **Latent Lane** (research). Communication between LLM agents through shared KV caches instead of decoded text, with a benchmark package and a whitepaper.

## Tools I use

Python · TypeScript · FastAPI · Vue · React · Azure AI Foundry · Fireworks AI · Inspect · LoRA fine-tuning · Swift
