# 🚀 Lyncs Agentic AI - Complete System Architecture

> **Version**: 3.0 (Smart Colleague Edition)  
> **Last Updated**: January 22, 2026  
> **Project**: Lyncs ERP AI Automation System  
> **Status**: Production-Ready Agentic System with Human-in-the-Loop Autopilot

---

## 📋 Table of Contents

1. [Executive Summary](#-executive-summary)
2. [System Overview](#-system-overview)
3. [Architecture Layers](#-architecture-layers)
4. [Technology Stack](#-technology-stack)
5. [Backend Architecture](#-backend-architecture---the-brain)
6. [Frontend Architecture](#-frontend-architecture---the-body)
7. [Agent System](#-agent-system)
8. [Autopilot Engine](#-autopilot-engine)
9. [Smart Colleague Protocol](#-smart-colleague-protocol)
10. [RAG System](#-rag-system)
11. [WebSocket Communication](#-websocket-communication)
12. [Data Flow](#-data-flow)
13. [Performance Optimizations](#-performance-optimizations)
14. [Security & Authentication](#-security--authentication)
15. [Module Support](#-module-support)
16. [Deployment](#-deployment)

---

## 🎯 Executive Summary

**Lyncs Agentic AI** is a sophisticated voice-controlled, browser automation system that enables **zero-manual-interaction** workflows across your entire ERP platform. Think of it as a "Smart Colleague" - an AI that understands intent, plans carefully, asks for confirmation, and executes with real-time commentary.

### Core Capabilities

| Capability | Description |
|------------|-------------|
| **🧠 Multi-Step Workflows** | "Onboard Zaki from Dubai" → Auto navigates, fills forms, submits |
| **👁️ Virtual Vision** | No screenshots - uses semantic DOM understanding |
| **⚡ Ultra-Fast** | Llama 3.1 8B on Groq (600+ tokens/sec, <200ms latency) |
| **🔄 Stateful Memory** | Remembers conversation context across sessions |
| **📚 RAG-Powered** | Answers questions using your private PDFs/documents |
| **🤝 Human-in-the-Loop** | Proposes plans, asks confirmation, allows refinement |
| **🌐 Bilingual** | Full English + Arabic support |

### What Makes It Special?

```
Traditional Automation       vs.      Lyncs Agentic AI
─────────────────────────          ─────────────────────────
Screenshots + OCR                   Virtual Vision (JSON)
Pre-scripted paths                  Dynamic AI planning
Breaks on UI changes               Semantic understanding
Single-step commands               Multi-step workflows
Silent execution                   Real-time commentary
No confirmation                    Human-in-the-loop
```

---

## 🏗️ System Overview

### High-Level Architecture Diagram

```
┌─────────────────────────────────────────────────────────────────────┐
│                           USER LAYER                                │
│                    Voice / Text / Chat Input                        │
└────────────────────────────────┬────────────────────────────────────┘
                                 │
┌────────────────────────────────▼────────────────────────────────────┐
│                      PRESENTATION LAYER                              │
│  ┌──────────────────────────────────────────────────────────────┐   │
│  │                   FRONTEND (React 18)                         │   │
│  │  ┌─────────────┐  ┌─────────────┐  ┌─────────────────────┐   │   │
│  │  │ VoiceControl│  │ DOM Scanner │  │ Action Executor     │   │   │
│  │  │   + Chat    │  │ (Vision)    │  │ (DOM Manipulation)  │   │   │
│  │  └──────┬──────┘  └──────┬──────┘  └─────────┬───────────┘   │   │
│  │         │                │                    │               │   │
│  │         └───────────┬────┴──────────┬────────┘               │   │
│  │                     │               │                         │   │
│  │           ┌─────────▼───────────────▼──────────┐             │   │
│  │           │      useAutopilot Hook             │             │   │
│  │           │  (Execution Engine + State Machine)│             │   │
│  │           └─────────────────┬──────────────────┘             │   │
│  └─────────────────────────────┼────────────────────────────────┘   │
└────────────────────────────────┼────────────────────────────────────┘
                                 │ WebSocket / REST
┌────────────────────────────────▼────────────────────────────────────┐
│                      INTELLIGENCE LAYER                              │
│  ┌──────────────────────────────────────────────────────────────┐   │
│  │                   BACKEND (FastAPI)                           │   │
│  │  ┌─────────────────┐  ┌─────────────────┐  ┌──────────────┐  │   │
│  │  │   Orchestrator  │  │ Autopilot       │  │ RAG Engine   │  │   │
│  │  │   Agent         │  │ Planner         │  │ (Knowledge)  │  │   │
│  │  │ (Intent + Plan) │  │ (Multi-Step)    │  │              │  │   │
│  │  └────────┬────────┘  └────────┬────────┘  └──────┬───────┘  │   │
│  │           │                    │                   │          │   │
│  │           └─────────────┬──────┴──────────┬───────┘          │   │
│  │                         │                 │                   │   │
│  │           ┌─────────────▼─────────────────▼────────────┐     │   │
│  │           │           LangGraph Agent                   │     │   │
│  │           │  (Stateful Workflow + Tool Execution)       │     │   │
│  │           └────────────────────┬───────────────────────┘     │   │
│  └────────────────────────────────┼─────────────────────────────┘   │
└────────────────────────────────────┼────────────────────────────────┘
                                     │
┌────────────────────────────────────▼────────────────────────────────┐
│                          AI LAYER                                    │
│  ┌────────────────────┐  ┌────────────────────┐  ┌──────────────┐   │
│  │   Groq Cloud       │  │   Qdrant           │  │ SQLite       │   │
│  │ (Llama 3.1 8B)     │  │ (Vector DB)        │  │ (Chat History)│   │
│  │                    │  │                    │  │              │   │
│  │ • Planning LLM     │  │ • Document Embeddings│ │ • Sessions   │   │
│  │ • Routing LLM      │  │ • Semantic Search  │  │ • Memory     │   │
│  │ • Generation LLM   │  │ • PDF Knowledge    │  │              │   │
│  └────────────────────┘  └────────────────────┘  └──────────────┘   │
└─────────────────────────────────────────────────────────────────────┘
                                     │
┌────────────────────────────────────▼────────────────────────────────┐
│                          DATA LAYER                                  │
│  ┌────────────────────────────────────────────────────────────────┐ │
│  │               ERP Backend (Node.js)                             │ │
│  │   PostgreSQL  •  User Data  •  Projects  •  Maintenance        │ │
│  └────────────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────────────┘
```

---

## 📚 Architecture Layers

### Layer 1: Presentation (Frontend)

| Component | Purpose | Technology |
|-----------|---------|------------|
| **VoiceControl** | Voice capture + text input | Web Speech API |
| **DoubtBot** | Chat UI + confirmation cards | React Components |
| **DOM Scanner** | Semantic page understanding | Custom Hook |
| **Action Executor** | Safe DOM manipulation | TypeScript |
| **Autopilot Hook** | Multi-step execution engine | React Hook |

### Layer 2: Intelligence (Backend)

| Component | Purpose | Technology |
|-----------|---------|------------|
| **Orchestrator Agent** | Intent classification + planning | Python + LangChain |
| **Autopilot Planner** | Multi-step workflow generation | Custom Logic |
| **RAG Engine** | Document search + Q&A | Qdrant + FastEmbed |
| **LangGraph Agent** | Stateful conversation flow | LangGraph |
| **WebSocket Router** | Real-time bidirectional comms | FastAPI |

### Layer 3: AI Services

| Service | Purpose | Provider |
|---------|---------|----------|
| **LLM** | Reasoning + Planning | Groq (Llama 3.1 8B) |
| **Embeddings** | Text vectorization | FastEmbed (Multilingual) |
| **Vector Search** | Semantic similarity | Qdrant |
| **Voice** | Voice-to-Voice (Optional) | OpenAI Realtime API |

### Layer 4: Data

| Store | Purpose | Technology |
|-------|---------|------------|
| **ERP Database** | Business data | PostgreSQL |
| **Vector Database** | Document knowledge | Qdrant |
| **Chat History** | Conversation memory | SQLite |

---

## 💻 Technology Stack

### Backend (`lyncs-ai`)

```yaml
Runtime: Python 3.11+
Framework: FastAPI
Agent Framework: LangGraph + LangChain
LLM Provider: Groq Cloud
  Model: llama-3.1-8b-instant
  Speed: 600+ tokens/second
  Latency: <200ms

Vector Database: Qdrant
Embedding Model: sentence-transformers/paraphrase-multilingual-MiniLM-L12-v2
  Dimensions: 384
  Languages: English + Arabic

PDF Processing: 
  - PyMuPDF (text extraction)
  - RapidOCR (scanned documents)

WebSocket: FastAPI native
Database: SQLite (chat history)
```

### Frontend (`Lyncs-Frontend`)

```yaml
Framework: React 18 + TypeScript
Build Tool: Vite
Routing: React Router DOM v6
State Management: Zustand + React Query
Forms: React Hook Form
UI Components: shadcn/ui + TailwindCSS
WebSocket: Native WebSocket API
Voice: Web Speech API (+ optional OpenAI Realtime)

Testing: Jest + React Testing Library
Linting: ESLint + Prettier
```

---

## 🧠 Backend Architecture - The Brain

### Directory Structure

```
lyncs-ai/
├── app/
│   ├── main.py                    # FastAPI app + all endpoints
│   ├── autopilot.py               # Multi-step execution planner
│   ├── automation.py              # Module-specific automation helpers
│   ├── orchestrator_agent.py      # Smart Colleague orchestrator
│   ├── orchestrator_websocket.py  # Orchestrator WS handler
│   ├── ws_router.py               # Main WebSocket handler
│   ├── form_fill_endpoint.py      # Form JSON extraction
│   ├── maintenance.py             # Maintenance module logic
│   ├── user_agent.py              # User management logic
│   ├── pydantic_agents.py         # Type-safe agents (experimental)
│   │
│   ├── agent/                     # LangGraph Agent Core
│   │   ├── graph.py               # Workflow definition
│   │   ├── nodes.py               # Agent nodes (router, tools)
│   │   ├── state.py               # AgentState schema
│   │   ├── tools.py               # LangChain tools
│   │   └── healer.py              # Self-correction logic
│   │
│   ├── services/                  # External Services
│   │   ├── rag_engine.py          # RAG core implementation
│   │   ├── rag_service.py         # RAG utilities
│   │   ├── erp_api.py             # ERP API client
│   │   └── erp_proxy.py           # ERP proxy layer
│   │
│   ├── core/                      # Configuration
│   │   ├── config.py              # Environment config
│   │   └── database.py            # DB connections
│   │
│   ├── db/                        # Database
│   │   └── chat_history.py        # SQLite chat storage
│   │
│   ├── schemas/                   # Pydantic Models
│   │   └── *.py                   # Request/Response schemas
│   │
│   └── prompts/                   # System Prompts
│       └── *.py                   # LLM prompt templates
│
├── qdrant_db/                     # Vector database storage
├── requirements.txt               # Python dependencies
├── .env                           # Environment variables
└── main.py                        # Entry point
```

### Key Backend Components

#### 1. main.py - Central API Gateway

The "Central Nervous System" of the backend with all HTTP/REST endpoints:

```python
# Key Endpoints

POST /agent/plan
  → Receives DOM snapshot + user intent
  → Returns atomic action (Click/Type/Navigate)
  → Used by: DOM-based navigation agent

POST /agent/navigate
  → Receives natural language intent
  → Returns target route path
  → Example: "Fix machine" → "/maintenance"

POST /agent/form-fill
  → Receives natural language + form fields
  → Returns structured JSON for form filling
  → Example: "Name is Zaki" → {"full_name": "Zaki"}

POST /ask
  → RAG-powered Q&A endpoint
  → Searches knowledge base + returns answer

POST /upload-pdf
  → Ingests PDFs into vector database
  → Uses OCR for scanned documents

WS /ws/neural-bridge
  → Real-time WebSocket for Autopilot
  → Bidirectional streaming
```

**SEMANTIC_ROUTES**: Contains 100+ route mappings for all ERP modules in both English and Arabic.

#### 2. autopilot.py - Multi-Step Planner

Generates complete execution plans for complex workflows:

```python
class ExecutionStep:
    order: int
    action: str     # NAVIGATE, WAIT_FOR_ROUTE, FILL_FORM, CLICK_ELEMENT, SUBMIT
    description: str
    route: Optional[str]
    payload: Optional[Dict]
    target: Optional[str]
    timeout_ms: int = 30000

class ExecutionPlan:
    plan_id: str
    goal: str
    steps: List[ExecutionStep]
    estimated_duration_ms: int

class AutopilotPlanner:
    async def plan(request, context, module) -> AsyncGenerator:
        # Pattern detection:
        # - "Onboard" → User creation workflow
        # - "Fix" → Maintenance ticket workflow
        # - "Create project" → Project creation workflow
```

**Entity Extraction**:
- **Names**: "Onboard Zaki" → `full_name: "Zaki"`
- **Emails**: Detects `@` symbols → `email: "..."`
- **Addresses**: "from Dubai" → `address: "Dubai"`
- **Nationalities**: "Saudi" / "Expat" patterns

#### 3. orchestrator_agent.py - Smart Colleague

The brain behind the Human-in-the-Loop workflow:

```python
class IntentClassifier:
    """Routes Q&A vs Actions"""
    ACTION_KEYWORDS = ["create", "add", "onboard", "update", "delete", "fix"]
    QUESTION_KEYWORDS = ["how", "what", "why", "explain", "help"]

class OrchestratorAgent:
    """State machine coordinator"""
    States: IDLE → PLANNING → WAITING_CONFIRMATION → EXECUTING → COMPLETE

class DraftPlan:
    """Plan structure for confirmation"""
    plan_id: str
    intent_summary: str
    module: str
    extracted_data: Dict
    steps: List[PlanStep]
    confidence: float
    requires_confirmation: bool
```

#### 4. ws_router.py - WebSocket Engine

Handles real-time bidirectional communication:

```python
# Message Types

# Client → Server
PROCESS_INTENT    # User request
CONTEXT_UPDATE    # Virtual vision data
STEP_COMPLETE     # Execution acknowledgment
PLAN_FAILED       # Error reporting

# Server → Client
STATUS            # "Analyzing..."
THINKING          # "Detected workflow..."
EXECUTE_PLAN      # Full multi-step plan
UPDATE_FORM       # Form field updates
NAVIGATE          # Route change command
THOUGHT           # Real-time commentary
STEP_COMPLETE     # Step finished
```

**Specialist Agents** (per module):
- `UserManagementAgent` - User/employee workflows
- `ProjectManagementAgent` - Construction projects
- `MaintenanceAgent` - Ticket creation
- `GreetingAgent` - Greeting card automation

#### 5. agent/graph.py - LangGraph Workflow

Stateful conversation management:

```python
# Workflow Flow
1. context_loader → Load user context (role, name, route)
2. router_node    → LLM decides: tool_call OR final_answer
3. [Conditional]  → tools → Execute (fetch_erp_stats, search_docs, fill_form)
4. [Loop]         → tools → router → Continue until done
5. END            → Return final response
```

**AgentState Schema**:
```python
class AgentState(TypedDict):
    messages: List[BaseMessage]      # Chat history
    user_context: Dict               # {role, name, token}
    current_route: str               # Current page path
    next_action: str                 # Router decision
    perf_metrics: Dict[str, float]   # Latency tracking
```

---

## 🎨 Frontend Architecture - The Body

### Directory Structure

```
Lyncs-Frontend/src/
├── components/
│   ├── AI/                        # AI-specific components
│   │   ├── ConfirmationCard.tsx   # Plan preview + confirmation
│   │   └── LiveStatusFeed.tsx     # Real-time execution feed
│   │
│   ├── VoiceControl.tsx           # Main voice controller
│   ├── ActionExecutor.tsx         # DOM manipulation
│   └── DoubtBot.tsx               # Chat widget UI
│
├── hooks/
│   ├── useAutopilot.ts            # Multi-step execution engine
│   ├── useDOMScanner.ts           # Semantic DOM scanner
│   ├── useVirtualVision.ts        # Context broadcaster
│   ├── useERPWebSocket.ts         # WebSocket client
│   ├── useFormBrain.ts            # Form intelligence
│   └── useAutomationExecutor.ts   # Action execution
│
├── contexts/
│   └── WebSocketContext.tsx       # Global WS state
│
├── apis/                          # API clients
├── pages/                         # Route components
├── routes/                        # Route definitions
└── utils/                         # Utilities
```

### Key Frontend Components

#### 1. VoiceControl.tsx - The Controller

Central orchestrator for voice/text commands:

```typescript
// The Agent Loop (max 6 iterations)
async function agentLoop(userIntent: string) {
  let iteration = 0;
  const MAX_STEPS = 6;
  
  while (iteration < MAX_STEPS) {
    // 1. Scan DOM (Virtual Vision)
    const snapshot = await scanDOM();
    
    // 2. Send to backend for planning
    const action = await planWithAI(userIntent, snapshot);
    
    // 3. Execute action
    await executeAction(action);
    
    // 4. Safety checks
    if (urlChanged || goalAchieved) break;
    
    iteration++;
  }
}

// Hybrid Navigation Strategy
if (KEYWORD_MAP[input]) {
  navigate(KEYWORD_MAP[input]);  // Fast path: 0ms
} else {
  const route = await aiNavigate(input);  // AI path: ~200ms
  navigate(route);
}
```

#### 2. useDOMScanner.ts - The Eyes

Converts complex web pages into AI-readable semantic snapshots:

```typescript
interface DOMElement {
  role: "button" | "input" | "link" | "select" | "textarea";
  label: string;
  selector: string;
  type?: string;
  value?: string;
  isVisible: boolean;
}

function scanDOM(): DOMElement[] {
  // 1. Query all interactive elements
  const elements = document.querySelectorAll(
    'button, input, a, select, textarea, [role="button"]'
  );
  
  // 2. Filter visibility
  const visible = [...elements].filter(el => {
    const rect = el.getBoundingClientRect();
    return rect.width > 0 && rect.height > 0 && isVisible(el);
  });
  
  // 3. Extract labels (aria-label, label tag, placeholder)
  // 4. Generate semantic snapshot
  // 5. Limit to ~40 items (context optimization)
  
  return semanticSnapshot;
}
```

#### 3. ActionExecutor.tsx - The Hands

Safe DOM manipulation with visual feedback:

```typescript
// Visual highlight before action
async function highlightElement(selector: string) {
  const element = document.querySelector(selector);
  element.style.outline = "3px solid red";
  element.style.outlineOffset = "2px";
  await sleep(500);  // User sees what's happening
}

// React-safe typing (critical!)
function typeIntoInput(element: HTMLInputElement, value: string) {
  // Standard .value = "text" doesn't trigger React onChange
  const setter = Object.getOwnPropertyDescriptor(
    HTMLInputElement.prototype,
    "value"
  )?.set;
  setter?.call(element, value);
  element.dispatchEvent(new Event("input", { bubbles: true }));
}

// Safety guard
function isSafeSelector(selector: string): boolean {
  const dangerous = ["div", "span", "body", "html"];
  return !dangerous.some(tag => selector === tag);
}
```

#### 4. useAutopilot.ts - The Robot Driver

Executes multi-step plans from the Autopilot Planner:

```typescript
interface AutopilotState {
  isExecuting: boolean;
  currentPlan: ExecutionPlan | null;
  executionQueue: ExecutionStep[];
  currentStepIndex: number;
  progress: number;  // 0-100
  statusMessage: string;
}

// Execution flow
async function executeStep(step: ExecutionStep) {
  switch (step.action) {
    case "NAVIGATE":
      navigate(step.route);
      break;
    case "WAIT_FOR_ROUTE":
      await waitFor(() => location.pathname === step.route, step.timeout_ms);
      break;
    case "FILL_FORM":
      Object.entries(step.payload).forEach(([key, value]) => {
        formSetValue(key, value);
      });
      break;
    case "CLICK_ELEMENT":
      document.querySelector(step.target)?.click();
      break;
  }
  
  // Report completion
  sendWebSocket({ type: "STEP_COMPLETE", step_order: step.order });
}
```

#### 5. useVirtualVision.ts - Context Broadcaster

Streams page state to backend (replaces screenshots):

```typescript
interface VirtualContext {
  route: string;
  available_fields: string[];
  form_values: Record<string, any>;
  available_buttons: string[];
  loading: boolean;
}

// Broadcast on changes
useEffect(() => {
  const context: VirtualContext = {
    route: location.pathname,
    available_fields: Object.keys(formFields),
    form_values: watch(),
    available_buttons: findButtons(),
    loading: isSubmitting
  };
  
  debouncedBroadcast(context);
}, [location.pathname, formValues, loading]);
```

---

## 🤖 Agent System

### LangGraph Agent Flow

```
┌─────────────────────────────────────────────────────┐
│                   User Message                       │
└────────────────────────┬────────────────────────────┘
                         │
                         ▼
┌─────────────────────────────────────────────────────┐
│              context_loader (Node 1)                 │
│  • Load user context (role, name, token)            │
│  • Inject current route                              │
│  • Set up performance tracking                       │
└────────────────────────┬────────────────────────────┘
                         │
                         ▼
┌─────────────────────────────────────────────────────┐
│               router_node (Node 2)                   │
│  • LLM analyzes message + context                   │
│  • Decides: TOOL_CALL or FINAL_ANSWER               │
│  • Token pruning (last 2 messages only)             │
└───────────────┬────────────────────┬────────────────┘
                │                    │
        [TOOL_CALL]           [FINAL_ANSWER]
                │                    │
                ▼                    ▼
┌───────────────────────┐   ┌────────────────────────┐
│    tool_node (Node 3) │   │        END             │
│  • fetch_erp_stats    │   │  Return response       │
│  • search_docs (RAG)  │   └────────────────────────┘
│  • fill_form          │
└───────────────┬───────┘
                │
                └─────────────────┐
                                  │
                                  ▼
                    ┌────────────────────────┐
                    │  Loop back to router   │
                    │  (with tool results)   │
                    └────────────────────────┘
```

### Available Tools

| Tool | Purpose | Returns |
|------|---------|---------|
| `fetch_erp_stats` | Get live ERP data | KPIs, counts, metrics |
| `search_docs` | RAG search in documents | Top 3 relevant chunks |
| `fill_form` | Extract form field data | Structured JSON |
| `navigate` | Determine target route | Route path string |

---

## 🛫 Autopilot Engine

### Workflow Patterns

#### Pattern 1: Onboarding/Creation

```
User: "Onboard Zaki from Dubai"

Detection:
✓ Keywords: "onboard" → Creation workflow
✓ Entity: "Zaki" → full_name
✓ Entity: "from Dubai" → address
✓ Target route: /users/new

Generated Plan:
┌────┬───────────────┬────────────────────────────────────┐
│ #  │ Action        │ Details                            │
├────┼───────────────┼────────────────────────────────────┤
│ 1  │ NAVIGATE      │ /users/new                         │
│ 2  │ WAIT_FOR_ROUTE│ timeout: 5000ms                    │
│ 3  │ FILL_FORM     │ {full_name: "Zaki", address: "Dubai"} │
│ 4  │ CLICK_ELEMENT │ [data-testid="submit_btn"]         │
└────┴───────────────┴────────────────────────────────────┘
```

#### Pattern 2: Maintenance Ticket

```
User: "Fix broken oven in kitchen"

Detection:
✓ Keywords: "fix", "broken" → Maintenance workflow
✓ Entity: "oven" → equipment_type
✓ Entity: "kitchen" → location

Generated Plan:
┌────┬───────────────┬────────────────────────────────────┐
│ #  │ Action        │ Details                            │
├────┼───────────────┼────────────────────────────────────┤
│ 1  │ NAVIGATE      │ /maintenance/new-ticket            │
│ 2  │ WAIT_FOR_ROUTE│ timeout: 5000ms                    │
│ 3  │ FILL_FORM     │ {equipment: "oven", location: "kitchen"} │
│ 4  │ CLICK_ELEMENT │ [data-testid="submit_ticket"]      │
└────┴───────────────┴────────────────────────────────────┘
```

#### Pattern 3: Navigation Only

```
User: "Go to maintenance tickets"

Detection:
✓ Keywords: "go to" → Navigation only
✓ Target route: /maintenance/tickets

Generated Plan:
┌────┬───────────────┬────────────────────────────────────┐
│ #  │ Action        │ Details                            │
├────┼───────────────┼────────────────────────────────────┤
│ 1  │ NAVIGATE      │ /maintenance/tickets               │
└────┴───────────────┴────────────────────────────────────┘
```

### Virtual Vision vs Computer Vision

| Feature | Traditional (Screenshots) | Lyncs (Virtual Vision) |
|---------|---------------------------|-------------------------|
| **Data Sent** | Images (MBs) | JSON (KBs) |
| **Processing** | OCR + Vision Models | Direct semantic access |
| **Speed** | Slow (image processing) | Instant (structured) |
| **Reliability** | Breaks on UI changes | Semantic understanding |
| **Privacy** | Screenshots leak data | No visual data sent |
| **Debugging** | Black box | Full JSON logs |

---

## 🤝 Smart Colleague Protocol

The Human-in-the-Loop workflow that makes AI a collaborative partner:

### State Machine

```
┌────────────────┐
│      IDLE      │◄────────────────────────────────┐
└───────┬────────┘                                 │
        │ User message                             │
        ▼                                          │
┌────────────────┐                                 │
│   CLASSIFYING  │                                 │
└───────┬────────┘                                 │
        │                                          │
        ├─── Q&A ──────► Answer directly ────────►─┘
        │
        ▼ ACTION
┌────────────────┐
│   PLANNING     │
└───────┬────────┘
        │ Draft plan ready
        ▼
┌────────────────────────┐
│ WAITING_CONFIRMATION   │◄─────────────┐
└───────┬────────────────┘              │
        │                               │
        ├─── Modify ──► Update plan ───►┘
        │
        ├─── Cancel ──► IDLE
        │
        ▼ Confirm
┌────────────────┐
│   EXECUTING    │
└───────┬────────┘
        │ All steps done
        ▼
┌────────────────┐
│   COMPLETE     │───────────────────►── IDLE
└────────────────┘
```

### Confirmation Card

When an action is detected, user sees:

```
┌──────────────────────────────────────────────────────┐
│ ✅ Proposed Action: Onboard user Zaki                │
│                                                       │
│ Extracted Data:                                       │
│ • full_name: Zaki                                     │
│ • address: Dubai                                      │
│                                                       │
│ Steps (4 actions):                                    │
│ 1. Navigate to User Creation page                     │
│ 2. Wait for page load                                 │
│ 3. Fill user details                                  │
│ 4. Submit user creation                               │
│                                                       │
│ Confidence: 92%        Est. Time: 10s                │
│                                                       │
│ [Confirm & Execute] [Modify Plan] [Cancel]           │
└──────────────────────────────────────────────────────┘
```

### Live Execution Feed

During execution, user sees:

```
┌──────────────────────────────────────────────────────┐
│ 🤖 Executing: Onboard user Zaki                      │
│                                                       │
│ [✓] Navigate to /users/new                           │
│ 💭 "Opening the user creation form..."               │
│                                                       │
│ [○] Filling form...                                  │
│ 💭 "Filling in all user information..."              │
│                                                       │
│ [ ] Submitting                                        │
│                                                       │
│ Progress: ████████░░░░░░░ 60%                        │
└──────────────────────────────────────────────────────┘
```

---

## 📚 RAG System

### Architecture

```
                    ┌───────────────┐
                    │  PDF Upload   │
                    └───────┬───────┘
                            │
                            ▼
                    ┌───────────────────────┐
                    │   PDF Processing      │
                    │  • PyMuPDF extract    │
                    │  • RapidOCR fallback  │
                    └───────┬───────────────┘
                            │
                            ▼
                    ┌───────────────────────┐
                    │   Text Chunking       │
                    │  • 500 char chunks    │
                    │  • Max 50 per doc     │
                    └───────┬───────────────┘
                            │
                            ▼
                    ┌───────────────────────┐
                    │   Embedding           │
                    │  • FastEmbed          │
                    │  • Multilingual       │
                    │  • 384 dimensions     │
                    └───────┬───────────────┘
                            │
                            ▼
                    ┌───────────────────────┐
                    │   Qdrant Storage      │
                    │  {content, url,       │
                    │   vector}             │
                    └───────┬───────────────┘
                            │
              ┌─────────────┴─────────────┐
              │                           │
              ▼                           ▼
    ┌─────────────────┐         ┌─────────────────┐
    │   User Query    │         │   Batch Query   │
    │   "What are     │         │   (Multiple     │
    │   safety rules?"│         │   documents)    │
    └────────┬────────┘         └─────────────────┘
             │
             ▼
    ┌─────────────────┐
    │ Semantic Search │
    │ TOP 3 matches   │
    └────────┬────────┘
             │
             ▼
    ┌─────────────────┐
    │ LLM Generation  │
    │ Answer with     │
    │ context         │
    └─────────────────┘
```

### Configuration

```python
EMBEDDING_MODEL = "sentence-transformers/paraphrase-multilingual-MiniLM-L12-v2"
VECTOR_DIMENSIONS = 384
CHUNK_SIZE = 500
MAX_CHUNKS_PER_DOC = 50
TOP_K_RESULTS = 3
```

---

## 🔄 WebSocket Communication

### Protocol Specification

```typescript
// Connection
ws://localhost:8000/ws/neural-bridge

// Client → Server Messages
interface ClientMessage {
  type: 
    | "PROCESS_INTENT"     // User request
    | "CONTEXT_UPDATE"     // Virtual vision data
    | "STEP_COMPLETE"      // Step finished
    | "PLAN_FAILED"        // Error occurred
    | "USER_MESSAGE"       // Chat message
    | "CANCEL_PLAN";       // Abort execution
  
  payload?: any;
}

// Server → Client Messages  
interface ServerMessage {
  type:
    | "CONNECTED"              // Connection established
    | "STATUS"                 // "Analyzing..."
    | "THINKING"               // "Detected workflow..."
    | "CONFIRMATION_REQUIRED"  // Show plan for approval
    | "EXECUTE_PLAN"           // Begin execution
    | "UPDATE_FORM"            // Update form fields
    | "NAVIGATE"               // Change route
    | "THOUGHT"                // Real-time commentary
    | "STEP_COMPLETE"          // Step finished
    | "EXECUTION_COMPLETE"     // All done
    | "ANSWER"                 // Q&A response
    | "ERROR";                 // Error occurred
    
  data?: any;
}
```

### Message Flow Example

```
CLIENT                                          SERVER
   │                                               │
   │────── PROCESS_INTENT ───────────────────────►│
   │       "Create user Zaki"                      │
   │                                               │
   │◄────── STATUS ────────────────────────────────│
   │        "Analyzing request..."                 │
   │                                               │
   │◄────── THINKING ──────────────────────────────│
   │        "Detected user creation workflow"      │
   │                                               │
   │◄────── CONFIRMATION_REQUIRED ─────────────────│
   │        {plan_id, steps, extracted_data}       │
   │                                               │
   │────── USER_MESSAGE ─────────────────────────►│
   │       "Yes, proceed"                          │
   │                                               │
   │◄────── EXECUTE_PLAN ──────────────────────────│
   │        {steps: [...]}                         │
   │                                               │
   │◄────── THOUGHT ───────────────────────────────│
   │        "Navigating to user form..."           │
   │                                               │
   │────── STEP_COMPLETE ────────────────────────►│
   │       {step_order: 1}                         │
   │                                               │
   │◄────── THOUGHT ───────────────────────────────│
   │        "Filling form fields..."               │
   │                                               │
   │────── STEP_COMPLETE ────────────────────────►│
   │       {step_order: 2}                         │
   │                                               │
   │◄────── EXECUTION_COMPLETE ────────────────────│
   │        {success: true}                        │
   │                                               │
```

---

## 🔀 Data Flow

### Complete Request Flow

**Scenario**: User says "Onboard Zaki from Dubai"

```
┌────────────────────────────────────────────────────────────────────┐
│ STEP 1: User Input                                                  │
│ Frontend captures: "Onboard Zaki from Dubai"                        │
│ Location: /dashboard                                                │
└────────────────────────────┬───────────────────────────────────────┘
                             │ WebSocket
                             ▼
┌────────────────────────────────────────────────────────────────────┐
│ STEP 2: Intent Classification                                       │
│ • Keywords: "onboard" → ACTION (not Q&A)                           │
│ • Module: USER_MANAGEMENT                                           │
│ • State: IDLE → PLANNING                                           │
└────────────────────────────┬───────────────────────────────────────┘
                             │
                             ▼
┌────────────────────────────────────────────────────────────────────┐
│ STEP 3: Entity Extraction                                          │
│ • "Zaki" → full_name                                               │
│ • "from Dubai" → address                                            │
│ • Confidence: 92%                                                   │
└────────────────────────────┬───────────────────────────────────────┘
                             │
                             ▼
┌────────────────────────────────────────────────────────────────────┐
│ STEP 4: Plan Generation                                             │
│ • Target route: /users/new                                          │
│ • Steps: NAVIGATE → WAIT → FILL_FORM → CLICK                       │
│ • State: PLANNING → WAITING_CONFIRMATION                           │
└────────────────────────────┬───────────────────────────────────────┘
                             │ CONFIRMATION_REQUIRED
                             ▼
┌────────────────────────────────────────────────────────────────────┐
│ STEP 5: User Confirmation                                           │
│ Frontend shows: ConfirmationCard with plan details                  │
│ User clicks: [Confirm & Execute]                                   │
└────────────────────────────┬───────────────────────────────────────┘
                             │ USER_MESSAGE: "Yes, proceed"
                             ▼
┌────────────────────────────────────────────────────────────────────┐
│ STEP 6: Execution Begins                                           │
│ • State: WAITING_CONFIRMATION → EXECUTING                          │
│ • Backend sends: EXECUTE_PLAN with all steps                       │
└────────────────────────────┬───────────────────────────────────────┘
                             │
                             ▼
┌────────────────────────────────────────────────────────────────────┐
│ STEP 7: Step 1 - Navigate                                          │
│ • Frontend: navigate("/users/new")                                 │
│ • Thought: "Opening the user creation form..."                     │
│ • Progress: 25%                                                    │
└────────────────────────────┬───────────────────────────────────────┘
                             │ STEP_COMPLETE
                             ▼
┌────────────────────────────────────────────────────────────────────┐
│ STEP 8: Step 2 - Wait for Route                                    │
│ • Frontend: waitFor(pathname === "/users/new")                     │
│ • Timeout: 5000ms                                                   │
│ • Progress: 50%                                                    │
└────────────────────────────┬───────────────────────────────────────┘
                             │ STEP_COMPLETE
                             ▼
┌────────────────────────────────────────────────────────────────────┐
│ STEP 9: Step 3 - Fill Form                                         │
│ • Frontend: setValue("full_name", "Zaki")                          │
│ • Frontend: setValue("address", "Dubai")                           │
│ • Thought: "Filling in all user information..."                    │
│ • Progress: 75%                                                    │
└────────────────────────────┬───────────────────────────────────────┘
                             │ STEP_COMPLETE
                             ▼
┌────────────────────────────────────────────────────────────────────┐
│ STEP 10: Step 4 - Submit                                           │
│ • Frontend: querySelector("[data-testid='submit_btn']").click()   │
│ • Thought: "Submitting the form..."                                │
│ • Progress: 100%                                                   │
└────────────────────────────┬───────────────────────────────────────┘
                             │ STEP_COMPLETE
                             ▼
┌────────────────────────────────────────────────────────────────────┐
│ STEP 11: Completion                                                 │
│ • Backend sends: EXECUTION_COMPLETE {success: true}                │
│ • State: EXECUTING → IDLE                                          │
│ • Frontend shows: Success toast                                    │
└────────────────────────────────────────────────────────────────────┘

Timeline: ~3-5 seconds total
```

---

## ⚡ Performance Optimizations

### Backend Optimizations

```python
# 1. Model Preloading (Saves ~15s on first request)
@app.on_event("startup")
async def startup():
    rag_engine.init_models()  # Load embedding model
    compile_llm()             # Initialize Groq client

# 2. LRU Caching (0ms for repeated queries)
@lru_cache(maxsize=128)
def get_embedding(text: str) -> List[float]:
    return embedding_model.embed([text])[0]

# 3. Token Pruning (Reduce cost + latency)
def router_node(state):
    messages = state["messages"]
    recent = messages[-2:]  # Keep only last 2 messages
    
    for msg in recent:
        if isinstance(msg, ToolMessage):
            msg.content = msg.content[:500] + "..."  # Truncate

# 4. Parallel Tool Execution
results = await asyncio.gather(
    smart_lookup("users", "full_name", "Zaki"),
    smart_lookup("stores", "name", "Dubai Mall")
)
```

### Frontend Optimizations

```typescript
// 1. Debounced Virtual Vision (prevent spam)
const debouncedBroadcast = useMemo(
  () => debounce((context) => ws.send(context), 300),
  []
);

// 2. Lazy Hook Initialization
const { isExecuting } = useAutopilot({
  enabled: location.pathname.includes('/new')
});

// 3. Progressive Status Updates
yield { type: "STATUS", message: "Analyzing..." };
await sleep(300);
yield { type: "THINKING", message: "Detected workflow..." };
```

### Measured Performance

| Metric | Value |
|--------|-------|
| **LLM Response** | <200ms (Groq Llama 3.1 8B) |
| **Embedding Search** | <50ms (Qdrant) |
| **ERP API Fetch** | 100-300ms (Node.js backend) |
| **Total Agent Response** | 250-500ms (end-to-end) |
| **Autopilot Plan Generation** | 500-800ms |
| **Step Execution** | 200-1000ms per step |

---

## 🔐 Security & Authentication

### Authentication Flow

```
┌─────────────┐     ┌──────────────┐     ┌─────────────┐
│   Frontend  │────►│   Lyncs-AI   │────►│  ERP Backend │
│             │     │   (FastAPI)  │     │  (Node.js)   │
└─────────────┘     └──────────────┘     └─────────────┘
       │                   │                    │
       │  Token in Header  │ Forward headers    │
       │  Authorization:   │ for validation     │
       │  Bearer <token>   │                    │
       └───────────────────┴────────────────────┘
```

### Backend Security

```python
# Header-based authentication
@app.post("/agent/plan")
async def plan(request: Request):
    headers = dict(request.headers)
    token = headers.get("authorization")
    
    # Validate token with ERP backend
    user_context = await validate_user(token)
    
    # Inject into agent state
    state["user_context"] = user_context
```

### CORS Configuration

```python
app.add_middleware(
    CORSMiddleware,
    allow_origins=["http://localhost:5173"],  # Frontend URL
    allow_credentials=True,
    allow_methods=["*"],
    allow_headers=["*"],
)
```

### WebSocket Authentication

```python
@router.websocket("/ws/neural-bridge")
async def websocket_endpoint(websocket: WebSocket):
    token = websocket.query_params.get("token")
    if not await validate_token(token):
        await websocket.close(code=4001)
        return
    await websocket.accept()
```

---

## 📊 Module Support

### Integrated Modules

| # | Module | Route | Automation Level |
|---|--------|-------|------------------|
| 1 | Dashboard | `/` | ✅ Navigation |
| 2 | User Management | `/users` | ✅ Full Autopilot |
| 3 | Projects | `/projects` | ✅ Full Autopilot |
| 4 | Business Intelligence | `/pulse` | ✅ Navigation + RAG |
| 5 | Assets | `/assets` | ✅ Navigation |
| 6 | IT Support | `/it-support` | ✅ Ticket Automation |
| 7 | Batch Control | `/batch-control` | ✅ Form Filling |
| 8 | Supply Chain | `/supply-chain` | ✅ Navigation |
| 9 | Audit | `/audit` | ✅ Navigation |
| 10 | QR Menus | `/qr` | ✅ Navigation |
| 11 | SOP | `/sop` | ✅ RAG Support |
| 12 | Greeting Cards | `/greeting` | ✅ Full Autopilot |
| 13 | Maintenance | `/maintenance` | ✅ Full Autopilot |

### Automation Levels

- **Navigation**: Can navigate to any page in the module
- **Form Filling**: Can auto-fill forms with extracted data
- **RAG Support**: Can answer questions from uploaded documents
- **Full Autopilot**: Complete end-to-end workflow automation

---

## 🚀 Deployment

### Quick Start Commands

#### Backend

```bash
cd lyncs-ai
python -m venv venv
.\venv\Scripts\activate      # Windows
source venv/bin/activate     # Linux/Mac
pip install -r requirements.txt
uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
```

#### Frontend

```bash
cd Lyncs-Frontend
npm install
npm run dev
```

### Environment Variables

**Backend (`.env`)**:
```env
GROQ_API_KEY=your_groq_api_key
NODE_BACKEND_URL=http://localhost:3000
QDRANT_HOST=localhost
QDRANT_PORT=6333
```

**Frontend (`.env`)**:
```env
VITE_AI_BACKEND_URL=http://localhost:8000
VITE_ERP_BACKEND_URL=http://localhost:3000
```

### Health Checks

```bash
# Backend
curl http://localhost:8000/docs    # OpenAPI docs
curl http://localhost:8000/health  # Health check

# Frontend
npm run dev                        # Dev server on :5173
```

---

## 🧠 Mental Model: The L-O-O-P

Remember **L-O-O-P** for understanding the agent cycle:

| Step | Letter | Action | Component |
|------|--------|--------|-----------|
| 1 | **L** | **Look** | Scan the DOM (Virtual Vision) |
| 2 | **O** | **One** | Plan ONE atomic action (Autopilot) |
| 3 | **O** | **Observe** | Watch the result (Step Complete) |
| 4 | **P** | **Proceed** | Stop if done, or loop again |

---



## 📚 Related Documentation

| Document | Purpose |
|----------|---------|
| `SMART_COLLEAGUE_PROTOCOL.md` | Human-in-the-loop details |
| `AUTOPILOT_ENGINE_README.md` | Autopilot deep dive |
| `WEBSOCKET_ENGINE_README.md` | WebSocket protocol spec |
| `AUTOPILOT_QUICKSTART.md` | Quick integration guide |
| `AUTOPILOT_REFERENCE.md` | API reference |

---

## 🛣️ Roadmap

### Completed ✅
- Multi-step Autopilot Engine
- Virtual Vision (DOM-based context)
- RAG with PDF ingestion
- WebSocket real-time streaming
- Specialist agents per module
- Human-in-the-Loop workflow
- Robust error handling

### In Progress 🚧
- Cross-page memory ("I saw settings on previous page")
- Scroll hunting for off-screen elements
- Self-correction loops (verify outcome)

### Planned 📝
- Vision API integration (Claude/GPT-4V)
- Multi-modal inputs (voice + screenshots)
- Intelligent retry with fallback selectors
- Analytics dashboard (plan success rates)
- OpenAI Realtime API voice mode

---

**Built with ❤️ for Enterprise ERP Automation**  
**Architecture Design**: Agentic AI with Human-in-the-Loop Autopilot  
**Version**: 3.0 (Smart Colleague Edition)  
**Last Updated**: January 22, 2026
