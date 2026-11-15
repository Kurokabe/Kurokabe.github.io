# Alain Gysi

**Machine Learning Engineer — Generative AI & ML Infrastructure**

Biel/Bienne, Switzerland · Swiss citizen, no work permit required
+41 79 236 78 06 · alain.gysi@outlook.com · [Portfolio](https://kurokabe.github.io) · [GitHub](https://github.com/Kurokabe) · [LinkedIn](https://www.linkedin.com/in/alain-gysi)

---

## Summary

Machine Learning Engineer with 6 years shipping production AI systems across industry and academic research. Specialized in generative models for visual modalities — images, video and 3D meshes — and in the infrastructure that trains and serves them: multi-GPU distributed PyTorch training, data pipelines over ~1M meshes, and 10x inference speedups with vLLM. Contributor to Darts, the 9.5k-star open-source forecasting library, where I built its model fine-tuning capability, published as an arXiv preprint. M.Sc. in Data Science, thesis graded 6.0/6.0.

---

## Work Experience

### Data & AI Engineer | Unit8
*September 2025 – Present | Lausanne / Zurich, Switzerland*

- Built the fine-tuning capability in Darts, the 9.5k-star open-source Python forecasting library, where PyTorch and foundation models could previously only be used as-is or trained from scratch; pretrained forecasters can now be adapted to a user's own data by freezing selected layers or fine-tuning end-to-end, removing the need to retrain from scratch for every new dataset.
- Built an LLM knowledge assistant for the finance team of a global leather chemicals company, turning the monthly Price-Volume-Mix (PVM) variance research behind its Board reporting into a conversation; analysts ask why sales moved against budget, forecast or prior year and get a board-ready answer with drivers and market context, cutting research that took each analyst 2–3 days per reporting cycle to about half a day (20–30 analyst-days freed per analyst per year).
- Designed the agent on Snowflake Cortex so the model never does the arithmetic: every figure comes from text-to-SQL over semantic views of a pre-computed PVM bridge, meeting the client's zero-calculation-error requirement, while hybrid search over industry newsletters supplies the market reasons behind each variance; tuned its analyst playbook through 5 evaluated iterations against a 36-question ground-truth set built from the finance team's own past reports.
- Took the assistant from prototype to a production-grade platform: dev, test and prod environments on Azure provisioned with Bicep, and a daily, re-runnable ingestion job into Snowflake that detects late month-end corrections and alerts the team rather than silently overwriting figures already presented to leadership.
- Co-built an LLM document translator for Switzerland's largest renewable energy producer, served as an MCP server on Azure inside the company's AI chat assistant: users attach a Word, PowerPoint, Excel or PDF file and download it translated, technical terms following a company glossary and the layout intact, turning a 50-page report that would take a professional translator about a week around in under a minute (a 300-page document in about 90 seconds).
- Solved the layout problem at the heart of the product, translations running up to a third longer than the boxes their source text filled: text is fitted through length budgets, font scaling floored at 80% and a single shorter rewording, while inline bold, italics and links travel through the model as numbered tags; rewrote the PDF pipeline to edit pages in place, raising its format preservation from 94% to over 99% so every test document clears the client's 95% target.
- Designed from scratch the Format Preservation Rate metric and the evaluation harness behind that target: a synthetic corpus generator (15 templates across Word, PowerPoint, Excel and PDF in 5 languages, covering all 20 language pairs), independent checks across five families from page structure to inline formatting, defect-injection tests proving every check catches the defect it targets, and baseline comparison that fails any change introducing a regression.
- Established data-lineage traceability across a large Swiss reinsurer's Palantir Foundry estate, where self-service Digital Services ingested data through data connections and third-party applications with no consolidated view of inflow and outflow; built the Foundry dataset that reconstructs that view, reverse-engineering undocumented Foundry APIs to extract metadata the platform did not expose, and put it in production on a daily rebuild.
- Closed the compliance loop on unmapped data sources: detected non-compliant data connections and third-party applications, generated the notification dataset driving automated emails to the owning Digital Service owner, and implemented automatic access revocation for sources left unmapped past 30 days, bringing a class of non-compliance the reinsurer's existing alerting stack did not cover under daily detection.

### Machine Learning Engineer | ORamaVR
*September 2023 – August 2025 | Geneva, Switzerland*

- Built the company's text- and image-to-3D generation stack by extending the MeshGPT transformer architecture and porting it into Hugging Face and NVIDIA NeMo, enabling conditioned mesh generation and editing for medical VR training content.
- Co-designed an octree-based mesh tokenization scheme that cut sequence length from 9 tokens per face to 3 (one per vertex), tripling the mesh complexity representable within a fixed context window, then tested and validated triangle-strip encoding for a further 50–60% reduction on top of that.
- Cut single-mesh generation from 5–10 minutes to 30–60 seconds (~10x) by rebuilding the test-time pipeline around vLLM with batching and memory optimizations, moving generation out of offline batch and into a range usable interactively.
- Designed the 3D data platform behind the generative stack: unit-box scaling, decimation, degenerate-face cleaning and multi-angle rendering across ShapeNet, MedShapeNet, Objaverse, Objaverse-XL and ShapeTalk, implemented with the Blender API, pymeshlab, trimesh and Kaolin and orchestrated with Metaflow; published each processed source as a versioned Hugging Face dataset with a custom loader, so training runs could select datasets and filter to single categories from config.
- Automated captioning of the mesh corpus by implementing the Cap3D methodology and substituting a locally hosted vision-language model (Ollama) for the paper's BLIP and ChatGPT stages, starting on LLaVA and moving to Gemma 3 for better caption quality on release, removing per-caption API cost and making text-conditioned training viable on a corpus far beyond what hand-labelling could reach; ran the full pipeline from mesh loading through cleaning, rendering, captioning and saving at roughly 30 seconds per mesh on a single 16-core workstation with one RTX 4090.
- Ran the full training and evaluation loop for the generative stack on a single 8×A100 node on Azure, using NVIDIA NeMo's multi-GPU training optimizations and Weights & Biases for experiment tracking; sole engineer on the workstream, presenting results and setting the next round of experiments with a supervising research scientist.
- Built the retrieval layer for a natural-language 3D scene generation tool: embedded mesh renders with CLIP and their generated captions with BERT, then served hybrid retrieval over both signals through PyVespa, letting an LLM assemble a scene by pulling matching assets from the processed corpus; extended scene export for direct use in Unity and Blender.

### Research Assistant | HE-Arc — University of Applied Sciences
*September 2020 – August 2023 | Neuchâtel, Switzerland*

- Delivered 7 applied ML projects for industry and public-sector partners across aerospace, manufacturing, finance, agriculture and urban mobility, taking each from client requirements through to a deployed model and handover.
- Improved satellite anomaly detection 15% over the rule-based system already in place at the European Space Agency (ESA), building an end-to-end PyTorch pipeline from preprocessing to deployment and integrating LIME and SHAP so engineers could trace which telemetry features drove each prediction, delivered with full handover documentation.
- Built a multi-agent reinforcement learning system for workshop production scheduling, migrating it from Unity ML-Agents (C#) to Ray RLlib with Ray Tune for reward-function and hyperparameter search; the trained agents reached the mathematically minimum number of production steps on every hand-computed scenario, including scenarios with mid-production machine breakdowns and with parallel orders of differing length.
- Developed a computer vision model with the Changins Viticulture Institute estimating grape cluster volume and weight from RGB-D images, segmenting bunches from cluttered vineyard backgrounds and extracting point-cloud features from depth maps; the PyTorch model outperformed both the analytic baseline and the classical ML approaches it replaced.
- Prepared the exercise notebooks for a Master's module on parallel programming in C++/CUDA, covering neural network distillation and TensorRT inference optimization, delivered to roughly 30 students per year across 2 years.

---

## Languages & Technologies

- **Machine Learning & AI:** PyTorch, PyTorch Lightning, Hugging Face Transformers, NVIDIA NeMo, DeepSpeed, vLLM, Ray (RLlib, Tune), scikit-learn, Weights & Biases
- **Generative & Multimodal:** LLMs, LLM agents (Snowflake Cortex Agents), MCP servers (FastMCP), text-to-SQL, diffusion models, vision-language models (LLaVA, Gemma), CLIP and SBERT embeddings, vector and hybrid search (Vespa, Cortex Search), retrieval-augmented generation, LLM evaluation, LangGraph, 3D mesh generation (MeshGPT, Kaolin, trimesh, Blender, USD)
- **Data & Infrastructure:** Docker, Kubernetes, Azure (Bicep, Container Apps, AI Foundry), AWS, Snowflake, document processing (PyMuPDF, python-docx, python-pptx, openpyxl), Airflow, Metaflow, PySpark, pandas, NumPy, CI/CD, distributed multi-GPU training
- **Programming Languages:** Python, C++ (CUDA, Qt), C#, SQL
- **Spoken:** French (native), English (C1, Cambridge First Certificate), Japanese (JLPT N2, self-taught), German (A2)

---

## Publications & Selected Projects

### [Unified Zero-Shot Time Series Forecasting: A Darts Foundation](https://arxiv.org/abs/2606.27438) | arXiv preprint, 2026
- Presents the foundation-model capabilities added to Darts, including the fine-tuning support I built that lets pretrained forecasters be adapted to user data through layer freezing or end-to-end training.

### [SOON: Social Network of Machines to Optimize Task Scheduling in Smart Manufacturing](https://ieeexplore.ieee.org/document/9569644) | IEEE PIMRC 2021
- Third author; published under the name F. Abdalla.
- Multi-agent reinforcement learning for production scheduling in a simulated manufacturing workshop, where agents reached the mathematically minimum number of production steps on every hand-computed scenario, including mid-production machine breakdowns and parallel orders of differing length.

### GANime — Video Generation with VQ-GAN and GPT-2 | M.Sc. Thesis, Osaka Metropolitan University
- Generated anime video sequences frame by frame conditioned on the first and last frame, combining a VQ-GAN for high-fidelity image synthesis with a GPT-2 transformer for frame prediction; graded 6.0/6.0.
- Reimplemented the full model from TensorFlow to PyTorch for deployment flexibility and reproducibility.
- **Technologies:** Python, PyTorch, PyTorch Lightning, TensorFlow, Hugging Face, Docker

---

## Education

**M.Sc. in Data Science** | HES-SO Master — University of Applied Sciences, Lausanne — 2019 – 2022
GPA 5.5/6.0 · Coursework completed 2020; thesis carried out at Osaka Metropolitan University, Japan in 2022 once COVID-19 border restrictions lifted, graded 6.0/6.0

**B.Sc. in Computer Science, Software Development** | HE-Arc — University of Applied Sciences, Neuchâtel — 2016 – 2019
GPA 5.6/6.0 · Award for best GPA of cohort

---

## Interests

Escape games, weightlifting, anime and manga

---
---

<!-- INTERNAL: everything below is working material, not CV content. Strip before sending. -->

# Project Bank (internal)

Fuller records than the role bullets above. Not for sending as-is: pick the entries matching a given
job description and compress them into role bullets. The **Best for** line is the filter.

### FP&A Knowledge Assistant: LLM Agent for Price-Volume-Mix Variance Analysis | Unit8, 2026

**Client naming:** "a global leather chemicals company" (Basel-headquartered). Do not name the client.

**Role:** Built most of the platform as part of a Unit8 team: Azure infrastructure, Snowflake ingestion and daily job, newsletter search, the agent's instructions, and the evaluation set and runner used to tune them. Integrated the existing PVM calculation into a single monthly pipeline with Snowflake-ready output; the core PVM business logic was largely colleagues' work.

**Problem:** Each month the finance team explains to leadership (executive team, Board) why sales moved against prior year, prior month, budget and forecast. Preparing that variance commentary took **2–3 days of manual research per analyst** per reporting cycle *(baseline from the client's requirements document)*, with inconsistent narrative quality and little carried over from one month to the next.

**Approach:**
- *Data:* Python pipeline computes the PVM bridge (six comparisons: month vs prior year, prior month, budget, forecast; YTD vs prior year, budget) from invoice lines, budget and forecast. Synced to Azure Blob, loaded into Snowflake by a daily job. Separate dev/test/prod environments provisioned with Bicep, governance tags, network policies.
- *Agent:* Snowflake Cortex Agent with text-to-SQL over four semantic views (PVM bridge, budget, forecast, invoice lines) plus Cortex Search over industry newsletters. Numbers always come from SQL, never from model arithmetic, which addresses the client's zero-calculation-error requirement.
- *Analyst playbook in the instructions:* asks for clarification when the period (month/YTD) or comparison basis is ambiguous; drills from market application to region to product category, then to customer/SKU level; grounds findings in newsletter commentary; says explicitly when the data cannot support a confident answer; replies in a fixed executive format (summary, variance table, drivers, context, recommendation).
- *Reliability:* incremental, re-runnable loads; late month-end invoice corrections are detected and emailed with the exact fix command instead of being silently applied.

**Evaluation:** 36-question ground-truth set built from the finance team's own past reports, covering narrative variance explanations, format compliance and out-of-scope questions. Scores both answer correctness and tool routing. Instructions went through 5 evaluated iterations, shaped by feedback from the client's finance lead.

**Results:**
- *Time:* 2–3 days → about half a day per analyst per month (~80% less), i.e. 20–30 analyst-days freed per analyst per year over 12 cycles.
- *Accuracy by design:* zero model-generated figures, every number traceable to a SQL query.

**Stack:** Python, pandas, Snowflake (Cortex Agents, Cortex Analyst, Cortex Search, semantic views), Azure Blob Storage, Bicep, Bash, SQL

**Best for:** AI engineering and applied LLM roles (primary): agents, text-to-SQL, RAG, LLM evaluation, enterprise data grounding. Also strong for data/analytics engineering and finance-sector roles. Pair with Shenlong to show retrieval work across two very different domains.

---

### AI Document Translator: Layout-Preserving LLM Translation | Unit8, 2026

**Client naming:** "Switzerland's largest renewable energy producer". Do not name the client.

**Role:** Team of four Unit8 engineers. Mine: the layout-fidelity work (overflow fitting for PowerPoint and PDF, inline-formatting markup, the PDF pipeline rewrite) and the whole evaluation framework (metric, corpus generator, checks, reporting, regression baselines). The MCP server, Azure infrastructure, glossary feature and load testing were teammates' work.

**Problem:** Staff work across German, French, Italian and English. Translating a report or a deck meant days of agency turnaround, or a generic tool followed by rebuilding the layout by hand. The client set a **Format Preservation Rate ≥ 95%** as a success criterion before the project started.

**Approach:**
- *Product:* an MCP server on Azure Container Apps, called from the company's AI chat assistant (Langdock). The document is parsed into text segments (JSON), translated by an LLM on Azure AI Foundry (EU data zone) in parallel batches with an optional glossary of technical terms, then written back into the original file.
- *Fitting (the hard part):* translations run longer than the source, and slide and PDF text sits in fixed-size boxes. Three steps: a length budget in the prompt (~110% of the source), font scaling down to 80% at most, then one request for a shorter rewording. PDFs are edited in place, so only the replaced text changes; page-bound Word sections keep their page count.
- *Inline formatting:* bold, italic, colour and links become numbered `<f1>…</f1>` tags, so the model moves the formatting with the words it wraps.

**Evaluation (designed and built alone):**
- *Format Preservation Rate (FPR):* lists every formatting feature of the original (bold span, image position, merged cell, font size…) and checks each in the translation, across five equally weighted families: structure, layout & fit, block style, inline formatting, objects. Untranslated text counts as n/a, not pass, so skipping content can't game the score; reported alongside translation coverage and text integrity (numbers, links, language).
- *Corpus:* generator of 15 templates (4 Word, 3 PowerPoint, 2 Excel, 6 PDF) in EN/DE/FR/IT/ES, in normal and "tight" densities where text fills its box: 26 documents per run, 130 for acceptance, all 20 ordered language pairs covered. Client documents kept as a confidential holdout, never used for tuning.
- *Trustworthiness:* a deterministic pseudo-translator for free, reproducible regression runs; defect-injection tests (removed bold, deleted image, moved box…) prove each check fires; baselines fail any change that regresses a document.
- *Findings:* surfaced a crash and about 20 classes of formatting failure across the four formats, written up for the team with file and line references.

**Results:**
- *PDF fidelity:* FPR 94% → over 99% (live runs: 94.3% with 1 of 3 documents passing → 99.6% with 3 of 3; 99.2% mean with 12 of 12 passing on the wider PDF set). Every PDF test document clears the 95% target.
- *Speed (team result):* a 310-page book translated in 89 seconds on the test environment; load test puts throughput at about 220 pages a minute, limited by the model quota.
- *Time vs. professional translation:* a 50-page report (~12,500 words) at ~2,500 words a day for a professional translator is about a week; the translator returns it in under a minute.

**Stack:** Python, FastMCP, Azure AI Foundry (GPT models), Azure Container Apps, PyMuPDF, python-docx, python-pptx, openpyxl, lxml, pytest

**Best for:** AI engineering and applied LLM roles: production LLM features beyond chat, MCP/tool integration, and especially **LLM evaluation** (designing a metric that can't be gamed and wiring it into regression gates). Also good for document-processing roles. Pair with the FP&A assistant to show two LLM products shipped for enterprise clients, each with its own evaluation.

---

### Mugiwara: Text- and Image-to-3D Mesh Generation | ORamaVR, 2023–2025

**Role:** Sole engineer on the workstream. A research scientist supervised experiment design and reviewed results.

**Objective** *(project intent, not a measured outcome)*: let VR content teams create 3D assets in hours rather than days, with the generator eventually embedded in ORamaVR's SDK. Integration was not confirmed before I left.

**Approach:** Extended the MeshGPT transformer architecture and ported it into Hugging Face and NVIDIA NeMo to support text and image conditioning and mesh editing. Co-designed an octree-based tokenization scheme with the research scientist. Trained on a single 8×A100 node on Azure, tracked in Weights & Biases.

**Results:**
- *Tokenization:* 9 tokens per face reduced to 3 (one per vertex), tripling the mesh complexity representable within a fixed context window. Triangle-strip encoding tested and validated for a further 50–60% reduction on top.
- *Inference:* single-mesh generation from 5–10 minutes down to 30–60 seconds (~10x), by rebuilding the test-time pipeline around vLLM with batching and memory optimizations. Moved generation out of offline batch and into interactive range.

**Research process:** Worked from the mesh-generation literature, reading papers and implementing the ideas. Explored Gaussian splatting as an alternative representation and rejected it: marching-cubes reconstruction produced meshes too large to be usable in VR.

**Stack:** PyTorch, NVIDIA NeMo, Hugging Face, vLLM, Weights & Biases, Azure

**Best for:** ML engineering roles (primary): generative modeling, transformer training infrastructure, inference optimization. Also strong for PhD applications in 3D generative modeling, where the tokenization contribution and the Gaussian splatting rejection together evidence a full research loop.

---

### OVR-Datasets: 3D Data Platform | ORamaVR, 2023–2025

**Role:** Sole engineer.

**Problem:** Training generative 3D models needs large, uniformly structured mesh corpora. Public 3D datasets vary widely in scale, orientation, face count and cleanliness, and carry no usable text annotations.

**Approach:** Built a processing pipeline covering unit-box scaling, decimation that reduces face count while preserving surface properties, degenerate-face removal and general mesh cleaning, plus multi-angle rendering to produce paired image data for image-to-3D. Implemented with the Blender API, pymeshlab, trimesh and Kaolin, parallelised with Metaflow. Published each processed source as a versioned Hugging Face dataset with a custom loader, so training runs could select datasets and filter to single categories from config.

**Corpora:** ShapeNet (55k), MedShapeNet (100k, medical), Objaverse (800k). ShapeTalk used separately for mesh editing, pairing a source and target mesh with an edit prompt such as *"the arms are longer and the legs shorter."* Objaverse-XL (10M) was available but not fully processed.

**Captioning:** Implemented the Cap3D methodology, substituting a locally hosted vision-language model via Ollama (LLaVA initially, then Gemma 3 on release for better caption quality) for the paper's BLIP and ChatGPT stages, removing per-caption API cost. Cap3D's internal CLIP-based best-of-5 view selection plus LLM summarization provided the quality mechanism. No separate formal evaluation was run beyond manual spot-checks during development, due to time constraints.

**Throughput:** Roughly 30 seconds per mesh end to end (load, clean, render, caption, save), parallelised, on a single workstation: 16-core i9 (24 threads) with one RTX 4090. Full processing ran continuously for 2–3 weeks.

**Known limits:** Meshes with millions of faces, such as landscape scans, were not usable.

**Stack:** Python, Blender API, pymeshlab, trimesh, Kaolin, Metaflow, Hugging Face Datasets, Ollama

**Best for:** ML engineering roles (primary): data pipelines for model training, large-scale preprocessing, MLOps, multimodal dataset construction. Pair with Mugiwara to show the full path from raw corpus to trained model to served inference.

---

### Shenlong: Retrieval-Augmented 3D Scene Generation | ORamaVR, 2023–2025

**Role:** Built the retrieval layer. The geometric algebra used for spatial placement was a colleague's work; I cleaned that code and extended scene export.

**Approach:** Embedded mesh renders with CLIP and their generated captions with BERT, then served hybrid retrieval over both signals through PyVespa. An LLM decomposes a natural-language request such as *"create a living room"* into the objects the scene needs, the retrieval layer returns matching assets from the processed corpus, and the placement stage arranges them in 3D. Supports iterative natural-language edits such as *"move the couch closer to the wall."* Scenes export for direct use in Unity and Blender.

**Stack:** Python, CLIP, BERT/SBERT, PyVespa, LLM APIs

**Best for:** AI engineering roles: RAG, multimodal retrieval, vector search, LLM application development. The one ORamaVR project that is not ML engineering, so lead with it only when the job description is about building on foundation models rather than training them.

---

### SOON-RL: Multi-Agent RL for Production Scheduling | CHIST-ERA / HE-Arc, 2019–2023

**Role:** Began as my Bachelor's thesis, built in C# with Unity ML-Agents and a custom UI for configuring workshop layouts. I then started my Master's, which COVID interrupted before the thesis phase; during that gap I joined HE-Arc as a Research Assistant and was asked to pick the project back up, since I already knew it. I migrated the framework from C#/Unity to Python for deeper algorithmic control and multi-agent scaling.

**Problem:** A workshop is a sequence of specialised machines producing parts to fulfil orders (A1 → B1 → C1). Machines must collaborate to complete orders in minimum time while adapting to disruption.

**Approach:** Built a custom simulation environment with Python, Gym and SimPy. Each machine agent chooses between Wait, Reconfigure, Fetch Parts and Produce, based on storage levels, production recipes, the current order, and the state and completion progress of every other machine. Migrated from Stable-Baselines to Ray RLlib to support multi-agent training, and used Ray Tune for hyperparameter and reward-function search.

**Result:** I hand-computed the minimum number of production steps required for each scenario, and the trained agents reached that minimum every time, across three scenarios of increasing difficulty:
- *Dynamic reconfiguration:* a new order arrives mid-production; agents decide whether to reconfigure immediately or after finishing the current order.
- *Fault tolerance:* a machine breaks down mid-production; the survivors reconfigure to compensate and prevent bottlenecks.
- *Parallel processing:* two simultaneous orders of differing length; agents shift resources from the completed short order to the longer one.

**Publication:** *SOON: Social Network of Machines to Optimize Task Scheduling in Smart Manufacturing*, IEEE PIMRC 2021. Third author, published as F. Abdalla.

**Stack:** Python, Ray RLlib, Ray Tune, Stable-Baselines, Gym, SimPy, Unity ML-Agents (C#)

**Best for:** RL roles, multi-agent systems, optimization and simulation. This is the only peer-reviewed publication with a verified optimality result, so lead with it for PhD applications and any RL-focused role.

---

### DL4Space: Satellite Telemetry Anomaly Detection | European Space Agency (ESA) / HE-Arc

**Role:** Built the anomaly detection system for the Assembly, Integration and Testing (AIT) phase.

**Problem:** Anomaly detection in satellite systems relied on rigid predefined rules. As satellite architectures grew more complex, rule maintenance became tedious and blind spots opened up. Worse, when a rule fired, engineers still had to hunt for the root cause by hand. The goal was not just to detect *when* something went wrong, but to explain *why*.

**Approach:** Architected a data engineering pipeline to clean, process and structure a large unstructured telemetry database, then designed a custom PyTorch model to classify anomalous events. Integrated SHAP to quantify each sensor and telemetry feature's contribution to a prediction, and LIME for localised human-readable explanations of individual anomalies, so engineers were not handed a black box.

**Result:** 15% improvement over the rule-based system already in place, delivered with full handover documentation.

> *Internal note:* the exact metric behind the 15% was not recorded. Probably F1, but do not claim a
> specific metric without verifying. The portfolio page says "accuracy"; the figure is deliberately
> left unqualified in the CV for this reason.

**Stack:** Python, PyTorch, SQL, SHAP, LIME

**Best for:** ML engineering roles involving time-series or anomaly detection, and any regulated or high-assurance domain where explainability is a requirement. Strong name recognition.

---

### MoDoS: Urban Mobility Hazard Classification | HEIG-VD / HE-Arc

**Role:** Designed, trained and deployed the computer vision engine.

**Problem:** A routing application for seniors and people with reduced mobility needed to identify street hazards from crowdsourced images. The data came from a local "Mapping Party" and was heavily imbalanced: overwhelmingly normal street scenes, very few actual hazards.

**Approach:** Fine-tuned MobileNetV2 in TensorFlow/Keras for real-time processing. To stop the model collapsing onto the majority class, engineered a two-stage cascade:
- *Stage 1, binary anomaly detection:* does the image contain a problem at all? **F1 0.81**
- *Stage 2, hazard categorisation* across seven classes (steep slopes, dangerous paths, narrow paths, obstacles, surface problems, missing curb ramps): **F1 0.90**
- *Combined pipeline:* **0.73**

**Deployment:** Containerised with Docker and served through TensorFlow Serving for high availability and low latency, integrated directly into the MoDoS user application.

**Stack:** Python, TensorFlow, Keras, TensorFlow Serving, Docker

**Best for:** computer vision roles, class-imbalance problems, and model deployment or serving. Also carries a genuine social-impact story, useful for mission-driven organisations.

---

### K-Défauts: Defect Classification from Engineer Notes | Ceramaret / HE-Arc

**Role:** Sole developer.

**Problem:** Ceramaret manufactures advanced ceramic components, and the fragility of ceramics caused roughly 10% material loss in production. Defect categorisation depended on free-text "notices of non-compliance" written by quality engineers, covering functional, dimensional, aesthetic and pollution-related problems. The data was entirely unlabelled.

**Approach:** Applied unsupervised clustering first, both to prove that distinct defect categories could be separated mathematically and to bootstrap a labelled set. Then built a supervised NLP classifier with scikit-learn and spaCy, using textual data augmentation to compensate for limited data. As the project scaled, moved to multi-label classification, since a single part can carry several defect types at once.

**Results:** Data augmentation raised weighted-average F1 from **0.64 to 0.73**. The final multi-label model reached **85% accuracy across seven defect categories**.

**Stack:** Python, scikit-learn, spaCy

**Best for:** NLP roles, text classification, and any problem starting from unlabelled data. The unsupervised-bootstrap-into-supervised progression is the transferable part, and it maps well onto manufacturing and quality analytics.

---

### Estigrappe3D: Grape Yield Estimation from RGB-D | Changins / HE-Arc

**Role:** Sole developer.

**Problem:** Estimating grape cluster volume and weight is manual and destructive. Changins, the university of viticulture and oenology, wanted it automated from depth imaging.

**Approach:** Integrated a masking model to segment grape bunches from cluttered vineyard backgrounds, extracted 3D point-cloud features from depth maps, and trained a custom PyTorch regression model to predict physical weight from the spatial representation.

**Result:** The PyTorch model outperformed both the analytic baseline and the classical ML approaches it replaced. Specific metrics were not recorded.

**Stack:** Python, PyTorch, point cloud processing, image masking

**Best for:** computer vision roles involving 3D or depth data, regression from sensor input, and agritech.

---

### Clustering Tool: Electricity Consumption Profiling | La Goule, St-Imier / HE-Arc

**Role:** Developer.

**Approach:** Clustering of electricity consumption data to identify distinct user profiles for a regional electricity provider.

**Stack:** Python

**Best for:** unsupervised learning and the utilities or energy sector.

> *Sparse entry.* No portfolio detail page exists (the card is commented out in `index.html`) and the
> details here are thin. Expand before using it, particularly if targeting an energy-sector role.

---

### PPI-Doppelganger: Financial Forecasting, then NLP Pivot | Perreard Partners Investments / HE-Arc

*Low priority. Include only for finance-sector roles.*

**Role:** Sole developer.

**Phase 1:** Built a time-series model in TensorFlow/Keras predicting currency pair trends from OHLC data, inflation indices and gold prices. Integrated SHAP and LIME so traders could see which market factors drove each prediction, since a black-box model is unusable in a trading context.

**Pivot:** Predictive accuracy plateaued and the model needed constant retraining to stay relevant. I recommended and executed a pivot with the client toward NLP: text classification, document summarisation, topic modelling and sentiment analysis over financial documents, bank reports and news, so traders could extract insight from dense sources rather than chase a marginal price signal.

> *Unverified figure:* the portfolio states accuracy was "capped at around 55%". Alain doubts this is
> right. Verify before using it anywhere, including on the portfolio page.

**Stack:** Python, TensorFlow, Keras, spaCy, SHAP, LIME

**Best for:** finance-sector roles only. The transferable signal is judgment rather than the model: recognising that an approach was not going to work and redirecting the engagement instead of continuing to grind on it.

---

## Tailoring notes

Variants to swap in depending on the target. This document is the master record; a sent CV is a
selection from it.

**Summary, data-scale clause**
- *Industry roles (current default):* "data pipelines over ~1M meshes"
- *PhD applications:* "data pipelines across ShapeNet, MedShapeNet and Objaverse" — names corpora an
  advisor recognises instantly and avoids a bare figure inviting a scale question.

**Summary, AI engineering variant**
- For applied LLM / AI engineering roles, add after the infrastructure clause: "and LLM agents
  grounded in enterprise data, including a text-to-SQL and RAG assistant that cuts a finance team's
  monthly variance research from days to hours."

**Emphasis by target**
- *AI engineering / applied LLM roles:* lead with the FP&A Knowledge Assistant (agent design,
  "model never does the arithmetic", evaluation loop) and the AI Document Translator (layout fitting,
  FPR metric), then Shenlong for retrieval. If space allows only one Unit8 LLM project, pick the
  translator for evaluation-heavy roles and the FP&A assistant for agent or data-heavy roles.
- *ML engineering roles:* lead with the data platform, training and evaluation loop, and the vLLM
  inference work. These are the closest match to the day-to-day of the role.
- *PhD applications:* lead with the octree tokenization contribution (a measurable architectural
  result, co-designed with a research scientist), the Cap3D adaptation, and the rejected Gaussian
  splatting exploration. Together they evidence a full research loop: read, adapt, implement,
  evaluate, and abandon what does not work.

**Claims deliberately excluded, and why**
- *"3D assets in hours instead of days"* — this was the project objective, never a verified outcome.
  Text-to-3D was intended for the SDK but integration was not confirmed before departure.
- *"Live production service"* for the mesh generation stack — same reason.
- *"5M+ meshes"* — the processed corpora (ShapeNet 55k, MedShapeNet 100k, Objaverse 800k) total
  roughly 1M. The arithmetic is checkable by any specialist reader.
- *"Removed N months of manual labelling"* (captioning) and *"replaced N hours/week of manual review"*
  (Unit8 compliance) — in both cases no manual baseline existed. The work created capability that was
  absent, which is the stronger and accurate claim.
- *Caption-quality percentage* — no formal evaluation was run, only manual spot-checks during
  development. Cap3D's internal CLIP-based best-of-5 selection is the quality mechanism.
- *FP&A assistant data volumes* (invoice lines, customers, materials) — only a few months were loaded
  at first and the team later added the full year, so any count is both uncertain and growing.
- *"Explains 80% of each variance"* — this was the client's requirement, never measured.
- *Usage or adoption figures* for the FP&A assistant — none recorded.
- *Translator: "≥ 95% format preservation across all formats"* — verified for PDF only. The one
  live run covering every format (before the later fixes) had Word 100%, PDF 93%, PowerPoint 84%,
  Excel 82%, and no later all-format live run exists.
- *Translator speed as a personal result* — the 89-second / 220-pages-a-minute figures come from
  teammates' performance work; use them to describe the product, not as something I optimised.
- *Translator business criteria examples* (8.2M CHF claims, 20,000 KYC scans, 7,000 briefs…) — these
  were sample metrics from other projects in the client's criteria template, not this project.
- *Translator usage or adoption figures* — none recorded.

**Still open**
- Whether the SwissRe engagement can be named, or must stay "a large Swiss reinsurer".
- Em dash sweep across prose (deferred).
- DL4Space: which metric the 15% refers to. Left unqualified in the CV until confirmed.
- PPI: the "55% accuracy" figure on the portfolio page is doubted and unverified.
- Clustering Tool (La Goule): entry is sparse and has no portfolio detail page.