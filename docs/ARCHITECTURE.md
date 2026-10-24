# SimpanAI — System Architecture & Block Diagram

## 1. Tech Stack Overview
| Layer | Technology | Role in SimpanAI |
| :--- | :--- | :--- |
| **Frontend** | TypeScript, Vite, Tailwind CSS, TanStack Query, Wouter | Displays the inventory dashboard, expiry/aging alerts, and replenishment approval controls. |
| **Backend** | TypeScript, Express 5 | Processes recorded sales, deducts stock counts, and checks safety stock limits and expiry dates. |
| **Database** | SQLite | Stores synthetic product records, safety limits, expiry dates, and historical sales data. |
| **AI / Compute** | RunPod (GPU) | Runs the AI sales forecasting model to predict future demand and suggest replenishment quantities. |
| **Hosting** | Replit | Cloud development environment and live web prototype hosting. |

## 2. System Block Diagram (5-Step Automated Workflow)
```mermaid
flowchart LR
    A[Frontend UI\nVite + Tailwind + TanStack Query] -->|1. Trigger: Log Sale / Scan Stock| B[Backend Engine\nTypeScript + Express 5]
    B <-->|2. Connected Data: Check Limits & Expiry| C[(Database\nSQLite)]
    B <-->|3. Decision Logic: Past Sales -> Forecast| D[AI Compute\nRunPod Serverless GPU]
    B -->|4. Human Approval: Suggest Resupply| A
    A -->|5. Visible Outcome: Approve / Manual Order| C
