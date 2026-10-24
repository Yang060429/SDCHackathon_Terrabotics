# SimpanAI

> A website for Malaysian SMEs for them to view and manage their stock inventory without using different platforms.

---

## Team Information

| Field                  | Details                                     |
| ---------------------- | ------------------------------------------- |
| **Team Name**          | TerraBotics                                 |
| **Team Domain**        | Domain 2                                    |
| **SDG Track (1–17)**   | SDG 8: Decent Work and Economic Growth and SDG 9: Industry, Innovation and Infrastructure |
| **Team Leader**        | Lo Yu Ao                                    |
| **University**         | Xiamen University Malaysia                  |
| **Number of Members**  | 5                                           |

## Links

| Resource          | Link                                                   |
| ----------------- | ----------------------------------------------         |
| GitHub Repository | https://github.com/Yang060429/SDCHackathon_Terrabotics |
| Live Demo         | https://SimpanAI.replit.app                            |
| RunPod Endpoint   | -                |
| Slide Deck        | https://canva.link/fjh69ml643f0i59                     |
| Demo Video        | https://example.com/demo-video                         |

---

## Overview

### Problem

As traditional shopping shifts toward online platforms, Malaysian SMEs struggle to manage inventory, relying on disconnected spreadsheets, paper records, and WhatsApp messages. Without automated tracking, staff frequently overlook depleting stock counts leading to sudden stockouts, while items left sitting in storage expire or degrade. This serious problem drains SME cash flow, creates avoidable material waste, and causes burnout for owners and staff spending evenings on repetitive manual tracking.

### Solution

Built using Replit within the Orbyte ecosystem, our web application provides an intuitive inventory management and automated replenishment module that automatically deducts sold quantities from live inventory. As stock levels change, the platform continuously monitors inventory health to trigger alerts for low or aging stock, integrating AI predictive modeling to forecast sales and calculate optimal replenishment quantities. To ensure people stay in control, the system requires explicit human approval for AI suggestions, combining SDC Phase 1 skills to prevent costly stockouts and expiration waste without complex staff training.

### Key Features

- **Feature 1** — Visual Inventory Management.
- **Feature 2** — AI Prediction for sales in future days.
- **Feature 3** — Provide user to order, Inbound and Outbound products more conviniently.

### Tech Stack

| Layer         | Technology                     |
| ------------- | ------------------------------ |
| Frontend      | TypeScript, Vite, Tailwind CSS, TanStack Query, Wouter |
| Backend       | TypeScript, Express 5, REST API          |
| Database      | SQLite                         |
| AI / Compute  | RunPod (GPU)                   |
| Hosting / Dev | Replit                         |

---

## Project Structure

```
.
├── docs/                    # Screenshots, diagrams
│   ├── Screenshots
│          ├── Forecasting.png
│          ├── History.png
│          ├── InventoryManage.png
│          ├── InventoryView.png
│          ├── Overview.png
│          └── Resupply.png
├── runpod/
│   └── handler.py           # RunPod serverless handler (GPU workload)
├── src/
│   ├── ml              # Application entry point
│       ├── __pycache__
│          └── trained_adapter.cpython-313.pyc
│       ├── original
│          ├── Try.py
│          ├── baseline.py
│          ├── check_gpu.py
│          ├── config.py
│          ├── data_utils.py
│          ├── deep_model.py
│          ├── evaluate.py
│          ├── train.py
│          ├── tree_model.py
│          └── windows.py
│       ├── requirements-trained.txt
│       └── trained_adapter.py
│   ├── scripts
│       ├── node_modules
│       ├── src
│          └── hello.ts
│       ├── package.json
│       ├── post-merge.sh
│       ├── tsconfig.json
│       └── tsconfig.tsbuildinfo
│   ├── .npmrc
│   ├── .replitignore
│   ├── ml_service.py
│   ├── package.json
│   ├── pnpm-lock.yaml
│   ├── pnpm-workspace.yaml
│   ├── replit.md
│   ├── tsconfig.base.json
│   └── tsconfig.json
├── submission/              # Required submission documents
│   ├── SDC2026_TerraBotics_Preliminary.pdf      # Preliminary submission
│   ├── SDC2026_TerraBotics_TechDeclaration.pdf  # Technology declaration
│   ├── SDC2026_TerraBotics_Replit_POU.pdf       # Replit proof of use
│   └── SDC2026_TerraBotics_Runpod_POU.pdf       # RunPod proof of use
├── tests/
│   └── test_utils.py        # Unit tests
├── .env.example             # Example environment variables
├── .gitignore
├── .replit                  # Replit run configuration
├── LICENSE
├── requirements.txt         # Python dependencies
├── README.md
└──requirements.txt
```

### Architecture

```
[Offline Training Phase]
RunPod (GPU Pod) ---> Train PyTorch Model ---> Export .pt weights ---> Load into Replit

[Live Application Phase]
User ---> Replit (Frontend App / API) ---> Local Model Inference (Replit Backend)
          |
          L---> Response returned to user
```

---

## How to Run

### Option 1 — Run on Replit

1. Open the [Replit Project](https://replit.com/@your-username/your-project), or import this repository via **Create Repl → Import from GitHub**.
2. Open the **Secrets** tab (🔒) and add the variables listed in `.env.example`:
   - `RUNPOD_API_KEY`
   - `RUNPOD_ENDPOINT_ID`
3. Click **Run**. Replit uses the `.replit` file to start `python src/main.py`.

### Option 2 — Run Locally

```bash
# 1. Clone the repository
git clone https://github.com/your-username/your-project.git
cd your-project

# 2. Create and activate a virtual environment
python -m venv venv
source venv/bin/activate        # Windows: venv\Scripts\activate

# 3. Install dependencies
pip install -r requirements.txt

# 4. Configure environment variables
cp .env.example .env            # then fill in your values

# 5. Run the app
python src/main.py
```

### Run Tests

```bash
python -m unittest discover tests
```

---

## How We Use Replit

- **Development:** We utilized Replit as our primary cloud IDE, heavily leveraging the Replit Agent to rapidly prototype our full-stack application (frontend UI and backend integration).
- **Hosting:** The entire application is hosted live directly within the Replit environment, providing a seamless platform for running both our web interface and the Python-based model inference service.
- **Integration & Version Control:** We used Replit's built-in Git tools to seamlessly manage our codebase and push source code directly to our GitHub repository without manual file handling.

📄 Proof of use: [`submission/SDC2026_TerraBotics_Replit_POU.pdf`](submission/SDC2026_TerraBotics_Replit_POU.pdf)

## How We Use RunPod

- **Workload:** We utilized RunPod's high-performance GPU instances to train and fine-tune our PyTorch ensemble models for demand forecasting.
- **Setup:** A standard **RunPod GPU Pod** was deployed with a PyTorch environment to handle intensive data processing and model training workflows.
- **Integration:** After training on RunPod, the finalized model weights (`.pt` files) were exported and directly integrated into our Replit backend for local inference.

Example request:

```bash
curl -X POST https://api.runpod.ai/v2/$RUNPOD_ENDPOINT_ID/runsync \
  -H "Authorization: Bearer $RUNPOD_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"input": {"prompt": "Hello"}}'
```

📄 Proof of use: [`submission/SDC2026_TerraBotics_Runpod_POU.pdf`](submission/SDC2026_TerraBotics_Runpod_POU.pdf)

---

## Challenges & Learnings

- What challenges did you face, and how did you overcome them?

  The primary limitation is the 'cold start' problem: because the model highly relies on historical transaction data, predictions are less accurate for newly launched products with zero sales history or sudden, viral demand spikes not captured in our dataset. To mitigate these risks, we implemented a safety line function to relieve stress if a sudden demand strike happens, alongside a 'Manual Purchase' override. This human-in-the-loop approach ensures merchants always retain final decision-making authority to restock based on their own market intuition, minimizing the risk of AI-driven overstocking or stockouts.

- What did your team learn?

  We learned how to seamlessly integrate RunPod GPU model training with a Replit full-stack web application to build an end-to-end AI product. We also mastered managing large AI project repositories on GitHub by correctly filtering heavy dependencies and model weights. Finally, we learned to handle real-world business challenges like "cold starts" by incorporating uncertainty visualizations and human-in-the-loop interventions into our UI.

## Future Improvements

- [ ] Improvement 1

      The recorded time duration for the history was too short. The prediction model will be able to run better with the data of whole year.
- [ ] Improvement 2

      The amount of data for training is not enough, which affected the accuracy of the prediction model. A more completed dataset will been used in future for better accuracy. 

## Team

| Name        | Role                | GitHub                                   |
| ----------- | ------------------- | ---------------------------------------- |
| Lo Yu Ao | Team Lead / Model Training / AI / RunPod | [@loyuaooo](https://github.com/loyuaooo) |
| Kor Yu Shao | Frontend / Backend            | [@kys0629](https://github.com/kys0629) |
| Lim Shang Yang | Frontend / Backend         | [@Yang040629](https://github.com/Yang040629) |
| Adam Largui | Frontend / Backend         | [@El-Mascot](https://github.com/El-Mascot) |
| Liu Hong Ming | Model Training / AI / RunPod         | [@lcooopa](https://github.com/lcooopa) |

---

## Submission Checklist

- [√] Team name, domain (Domain 1 / Domain 2) and SDG track filled in
- [√] Slide deck link added
- [√] Demo video link added
- [√] Replit used, with proof of use in `submission/`
- [√] RunPod used, with proof of use in `submission/`
- [√] Preliminary submission completed (`SDC2026_TeamName_Preliminary.pdf`)
- [√] Technology declaration completed (`SDC2026_TeamName_TechDeclaration.pdf`)
- [√] Submission files renamed with your team name (replace `TeamName`)
- [√] "How to Run" steps verified
- [√] No API keys or secrets committed to the repository

## License

This project is licensed under the [Apache License 2.0](LICENSE).
