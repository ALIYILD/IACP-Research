# Inter-Agency Collaborative Practice (IACP) for AI Agents

[![arXiv](https://img.shields.io/badge/arXiv-2025.XXXXX-b31b1b.svg)](https://arxiv.org/abs/2025.XXXXX)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)

## Abstract

This repository contains the reference implementation for **Inter-Agency Collaborative Practice (IACP)**, a task-centred collaboration framework for multi-agent AI systems inspired by interprofessional teamwork models in healthcare.

IACP introduces a paradigm shift from agent orchestration to agent collaboration, where:
- **Mono-professional specialist agents** dynamically assemble around shared tasks
- A **facilitator agent** enables collaboration without centralizing domain expertise
- Intelligence emerges from structured interaction rather than centralized control

## Key Concepts

### The IACP Design Pattern

| Component | Description |
|-----------|-------------|
| **Task** | Central organizing entity with goals, constraints, and metrics |
| **Specialist Agent** | Autonomous unit with deep expertise in a narrow domain |
| **Facilitator Agent** | Enables collaboration, manages context, synthesizes outcomes |
| **Conflict** | Divergent recommendations treated as diagnostic signals |
| **Consensus** | Alignment achieved through structured negotiation |
| **CIE** | Central Intelligent Engine for learning and adaptation |

### IACP vs Traditional Orchestration

```
Orchestration:  Controller → Agent1, Agent2, Agent3 (command-based)
A2A:            Agent1 ↔ Agent2 ↔ Agent3 (emergent, unstructured)
IACP:           Facilitator ↔ [Specialist Agents] ↔ Task (facilitated collaboration)
```

### Architecture Comparison

| Feature | Orchestration | Agent-to-Agent | IACP |
|---------|--------------|----------------|------|
| Decision Confidence | Fixed | Variable | High |
| Explainability | Low (30%) | Medium (50%) | High (90%) |
| Single Point of Failure | Yes | No | No |
| Conflict Resolution | None | None | Formal |
| Dynamic Agent Addition | No | Yes | Yes |
| Learning from Outcomes | No | No | Yes (CIE) |

## Features Implemented

### 1. Core IACP Framework
- Task-centred collaboration
- Facilitator-guided coordination
- Mono-professional specialist agents

### 2. Central Intelligent Engine (CIE)
- Outcome tracking and evaluation
- Agent trust score adjustment
- Performance-based agent recommendations
- Closed-loop learning system

### 3. Iterative Collaboration
- Reassessment triggers
- Convergence criteria
- Strategy adaptation
- Non-linear problem solving

### 4. Enhanced Conflict Detection
All four conflict types from the paper:
- **Direct Contradiction** - Mutually exclusive recommendations
- **Resource Competition** - Competing for same resources
- **Priority Disagreement** - Different priority orderings
- **Constraint Violation** - Recommendations violating constraints

### 5. Multi-Task Participation
- Agents participating in multiple tasks concurrently
- Cross-task insight sharing
- Professional accountability tracking
- Context preservation

### 6. Architecture Comparison
- Side-by-side comparison with Orchestration and A2A
- Metrics: explainability, scalability, robustness

## Repository Structure

```
IACP-Research-Paper/
├── src/
│   ├── iacp/                        # Core IACP Framework
│   │   ├── __init__.py              # Package exports
│   │   ├── task.py                  # Task definition and management
│   │   ├── specialist_agent.py      # Base specialist agent class
│   │   ├── facilitator.py           # Facilitator agent implementation
│   │   ├── consensus.py             # Conflict detection & consensus
│   │   ├── cie.py                   # Central Intelligent Engine
│   │   ├── iterative.py             # Iterative collaboration
│   │   ├── comparison.py            # Architecture comparison
│   │   └── multi_task.py            # Multi-task coordination
│   └── examples/
│       └── digital_marketing_team/  # Demo implementation
│           ├── agents/              # 5 specialist marketing agents
│           │   ├── seo_specialist.py
│           │   ├── content_strategist.py
│           │   ├── social_media_manager.py
│           │   ├── analytics_expert.py
│           │   └── budget_controller.py
│           └── demo.py              # Comprehensive demonstration
├── docs/                            # Additional documentation
├── figures/                         # Paper figures and diagrams
├── requirements.txt                 # Dependencies
├── LICENSE                          # MIT License
└── README.md                        # This file
```

## Quick Start

### Installation

```bash
git clone https://github.com/yourusername/IACP-Research-Paper.git
cd IACP-Research-Paper
pip install -r requirements.txt  # No external deps required
```

### Running the Demo

```bash
# Full demonstration of all features
python -m src.examples.digital_marketing_team.demo

# Quick demo (basic IACP only)
python -m src.examples.digital_marketing_team.demo --quick
```

## Example: Digital Marketing Team

The demo implements a digital marketing team using IACP:

### Specialist Agents

| Agent | Domain Expertise |
|-------|------------------|
| **SEO Specialist** | Search engine optimization, keywords, rankings |
| **Content Strategist** | Content planning, messaging, storytelling |
| **Social Media Manager** | Platform strategy, engagement, community |
| **Analytics Expert** | Metrics, KPIs, data-driven insights |
| **Budget Controller** | Cost optimization, ROI, resource allocation |

### Demo Output

```
======================================================================
  DEMO 1: BASIC IACP COLLABORATION
======================================================================
[Facilitator] Initiating collaboration on: Launch marketing campaign
[Facilitator] Selecting relevant agents for task...
  + Engaged: SEO (seo_b351)
  + Engaged: Content Strategy (content_strategy_f78d)
  + Engaged: Social Media (social_media_ac5a)
  + Engaged: Analytics (analytics_d688)
  + Engaged: Budget Control (budget_control_e8c9)

[Facilitator] Gathering analyses from 5 agents...
[Facilitator] Collecting recommendations...
[Facilitator] Synthesizing recommendations...
[Facilitator] Consensus reached:
  Action: Implement measurement framework tracking: Impressions, Reach, CPM
  Confidence: 80%
  Contributing agents: 5
```

## Usage Examples

### Basic Collaboration

```python
from src.iacp import Task, FacilitatorAgent
from src.examples.digital_marketing_team.agents import *

# Create facilitator and register agents
facilitator = FacilitatorAgent(name="Marketing Facilitator")
facilitator.register_agent(SEOSpecialist())
facilitator.register_agent(ContentStrategist())
facilitator.register_agent(AnalyticsExpert())

# Create and execute task
task = Task(
    objective="Launch product marketing campaign",
    description="Build awareness for new SaaS product"
)
task.add_constraint("Budget", "Total budget", 15000)

resolution = facilitator.facilitate(task)
print(f"Decision: {resolution.action}")
print(f"Confidence: {resolution.confidence:.0%}")
```

### With Learning (CIE)

```python
from src.iacp import CentralIntelligentEngine

cie = CentralIntelligentEngine(learning_rate=0.2)

# Register agents for tracking
cie.register_agent("seo_agent", "SEO")
cie.register_agent("content_agent", "Content")

# After task completion, record outcome
cie.record_outcome(
    task_id="task_1",
    task_objective="Launch campaign",
    resolution_action="Execute SEO-first strategy",
    contributing_agents=["seo_agent", "content_agent"],
    predicted_confidence=0.8
)

# Evaluate actual outcome
cie.evaluate_outcome("task_1", actual_success=0.85)

# Get recommendations for future tasks
recommendations = cie.recommend_agents("New campaign", available_agents)
```

### Iterative Collaboration

```python
from src.iacp import IterativeCollaborator, ConvergenceCriteria

criteria = ConvergenceCriteria(
    min_confidence=0.75,
    max_iterations=5,
    consensus_ratio=0.6
)

iterative = IterativeCollaborator(facilitator, criteria)
resolution = iterative.iterate(task)

print(f"Converged after {iterative.current_iteration} iterations")
```

## Paper Concepts Mapped to Code

| Paper Concept | Code Module |
|--------------|-------------|
| Task as central entity | `task.py` - Task class |
| Mono-professional specialists | `specialist_agent.py` - SpecialistAgent |
| Facilitator (5 functions) | `facilitator.py` - FacilitatorAgent |
| Conflict as diagnostic signal | `consensus.py` - ConflictType enum |
| Consensus under constraint | `consensus.py` - ConsensusEngine |
| Central Intelligent Engine | `cie.py` - CentralIntelligentEngine |
| Iterative sense-making | `iterative.py` - IterativeCollaborator |
| Multi-task participation | `multi_task.py` - MultiTaskCoordinator |
| IACP vs Orchestration | `comparison.py` - ArchitectureComparison |

## Citation

If you use this code in your research, please cite:

```bibtex
@article{yildirim2025iacp,
  title={Inter-Agency Collaborative Practice for AI Agents},
  author={Yildirim, Ali},
  journal={arXiv preprint arXiv:2025.XXXXX},
  year={2025}
}
```

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## References

- Tran et al. (2025) - Multi-Agent Collaboration Mechanisms: A Survey of LLMs
- Krishnan et al. (2025) - Advancing Multi-Agent Systems Through Model Context Protocol
- Wu & Wang (2025) - GoalfyMax: A Protocol-Driven Multi-Agent System
- Bansod et al. (2025) - Distinguishing Autonomous AI Agents from Collaborative Agentic Systems
- Raza & Sapkota (2025) - TRiSM for Agentic AI
- Kostka & Chudziak (2025) - Cognitive Synergy
- Li & Ding (2025) - Dual Process Multi-scale Theory of Mind
