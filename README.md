# Financial Forensics Engine (RIFT Hackathon Edition)

A high-performance, web-based intelligence platform designed to expose money muling networks through advanced graph analysis, temporal windowing, and behavior-based scoring.

**🔗 Mandatory Links for Submission**:
- **Live Demo URL**: [INSERT VERCEL/RAILWAY URL HERE]
- **LinkedIn Video Post**: [INSERT LINKEDIN POST URL HERE]
- **GitHub Repository**: [INSERT GITHUB REPO URL HERE]

## 🚀 Tech Stack
- **Frontend**: React (Vite), Tailwind CSS, Lucide Icons, Vis-network (Graph Visualization)
- **Backend**: Python (FastAPI), Pandas, NetworkX
- **Analysis Engine**: Custom Python-based Graph Intelligence Module

## 🏗 System Architecture
The platform follows a decoupled client-server architecture:
1.  **Ingestion Layer**: Processes raw CSV data with fuzzy column mapping.
2.  **Graph Engine**: Constructs a directed multi-graph of all transactions.
3.  **Heuristic Layer**: Runs multiple detection passes (Cycles, Smurfing, Shell Chains).
4.  **Scoring Engine**: Aggregates pattern matches into a normalized Suspicion Score (0-100).
5.  **Visualization Layer**: Renders an interactive topology using a force-directed layout.

## 📂 Project Structure
```text
├── backend/            # FastAPI analytics server
│   ├── engine.py       # Core Graph Intelligence Module
│   ├── main.py         # API endpoints & data streaming
│   └── requirements.txt
├── frontend/           # React interactive dashboard
│   ├── src/
│   │   ├── components/ # GraphView, StatsDashboard, etc.
│   │   └── App.jsx     # Main Application state & UI logic
│   └── package.json
└── README.md           # Mandatory Documentation
```

## 📖 Usage Instructions

1.  **One-Click Start**: Run `START_SYSTEM.bat` (Windows) to initialize everything.
2.  **Forensic Command Center**: All critical controls are located in the top-right box.
    *   **Injest Data**: Upload your own CSV here.
    *   **Load Demo Data**: One-click to generate and auto-load a forensic dataset for your demo.
    *   **Risk Filter**: Real-time adjustment for high-risk node visibility.
3.  **Explore Topology**: Use the interactive graph to identify clusters. Red nodes represent high-risk accounts (>70%).
4.  **Simulation & Deep Dive**: Use the **Play** button for chronological replay and click nodes for **AI Forensic Reports**.
5.  **Download JSON**: Standardized RIFT report ready for submission.

## 🧠 Algorithm Approach & Complexity Analysis

### 1. Circular Fund Routing (Cycles)
- **Approach**: Uses Johnson’s algorithm (via NetworkX `simple_cycles`) to find circuits of length 3-5.
- **Optimization**: Search is restricted to a subgraph of non-legitimate entities with degree > 1.
- **Complexity**: $O((V+E)(c+1))$ where $c$ is the number of cycles. Depth-limiting ensures $O(V+E)$ performance on 10K datasets.

### 2. Smurfing (Fan-in / Fan-out)
- **Approach**: Sliding 72-hour window. Detects 10+ distinct sources (Fan-in) or destinations (Fan-out) within any 3-day window.
- **Complexity**: $O(N \log N)$ where $N$ is the transaction count, primarily driven by temporal sorting.

### 3. Layered Shell Networks
- **Approach**: Linear chain traversal identifying "bridge" accounts with strictly 2-3 transactions.
- **Complexity**: $O(V + E)$ (Breadth-First Search variant).

## 📊 Suspicion Score Methodology
The **Suspicion Score ($S$)** is a weighted aggregate capped at 100:
- **Smurfing (Fan-in/out)**: $+40$ pts (High-priority signal)
- **Cycles (Circuits)**: $+25$ pts
- **Shell Chains**: $+20$ pts
- **High Velocity/Bursts**: $+15$ pts

*False Positive Control: Nodes identified as merchants (50+ partners, consistent volume) or payroll (monthly cadence, stable amount) are whitelisted.*

## 🛠 Installation & Setup

### 🚀 Standard Setup (Recommended)
1.  **Extract** the project folder.
2.  **Double-click** `START_SYSTEM.bat`.
    *   This will install dependencies, start servers, and open the dashboard automatically.

### Manual Setup
1.  **Backend**: `cd backend && pip install -r requirements.txt && uvicorn main:app`
2.  **Frontend**: `cd frontend && npm install && npm run dev`

## ⚠️ Known Limitations
- Capped at 5-hop cycles for performance.
- Requires transaction timestamps for temporal windowing.

## 👥 Team Members
- **Abhay** - Lead Engineer (Full-Stack & Forensic Algorithms)
- **[Insert Other Team Members]**
