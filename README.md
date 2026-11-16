# Christian Bakhos

I build AI agents that take real actions, and the evaluations that show whether they are safe to deploy.

Most of my work is shipped for enterprise customers, so the code is private. The public project below shows how I work: frozen test sets, deterministic grading, and every number reproducible from the repo.

## Featured: [AccessFrontier](https://github.com/Christianb0011/access-frontier)

An agent harness and frozen benchmark for enterprise access (IAM) tickets, built in a hackathon on Fireworks AI.

**The problem.** An agent's reply can be correct while the action it executed was unsafe. In one recorded case, a frontier model granted payroll write access to a disabled user, revoked it, then replied "request refused". Answer-only evaluation scores that as a pass.

**What I built.** A cheap open model plus an agentic layer and a deterministic execution guard that blocks policy-violating writes before they reach production. I also built a 305-case held-out benchmark that grades the state change the agent made, not just its reply.

| | Strict score (main / hard) | Policy-violating writes | Cost per 10k tickets |
|---|---|---|---|
| Frontier model (GLM-5.3) | 90.5% / 81.9% | 3 | $36.27 |
| **My harness (GLM-5.3 Flash + guard)** | **99.0% / 99.0%** | **0** | **$4.19** |

Test sets, tools, policies, simulator and scorer are hash-locked before any run. A pre-commit hook blocks changes to them, train/test leakage and secrets. 47 of the 49 commits are mine.

## Other work (private: client or company code, walkthroughs on request)

- **Multi-agent maintenance planner for railways.** Six agents (orchestrator, asset history, spare parts, inventory, technicians, workshop slots) coordinate over the A2A protocol to produce maintenance proposals, with live progress streaming. Microsoft Agent Framework, FastAPI, Vue.
- **Claims-processing agent for a logistics company.** Reads monthly dispute files, applies business rules, checks parcel photos with a vision model, and recommends credit, no credit or review for each parcel. An analyst makes the final call.
- **Multilingual voice and text assistant for a science podcast.** Answers in Dutch, English or French with citations that link to episode timestamps. A Durable Functions pipeline transcribes and indexes new episodes. React 19, FastAPI, Azure AI Foundry, Voice Live, AI Search.
- **Voice-to-voice 3D avatar** for visitors at an innovation centre. Azure OpenAI Realtime API, lip sync, selectable personas, webcam-based visitor greeting.
- **Conservation kiosk with AI rhino identification** for a South African non-profit. Vue 3 on Azure Static Web Apps.
- **Latent Lane** (research). Communication between LLM agents through shared KV caches instead of decoded text, with a benchmark package and a whitepaper.

## Tools I use

Python · TypeScript · FastAPI · Vue · React · Azure AI Foundry · Fireworks AI · Inspect · LoRA fine-tuning · Swift
