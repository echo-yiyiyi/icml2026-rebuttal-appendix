# Rebuttal Appendix

## 1. CAMEL Components Ablation Study

#### Table 1. Reasoning Data Distillation Accuracy of GPT-4o-mini on high-difficulty (Level-5) MATH problems across six categories (50 randomly sampled questions per category).

| Category                  | Baseline (%) | TIR (%) |
|---------------------------|--------------|---------|
| Intermediate Algebra      | 20.0         | **36.0** |
| Precalculus               | 18.0         | **28.0** |
| Algebra                   | 70.0         | **80.0** |
| Counting & Probability    | 50.0         | **54.0** |
| Number Theory             | 54.0         | **62.0** |
| Prealgebra                | 58.0         | **66.0** |

#### Table 2. Performance Comparison on AIME Data Synthesis: CAMEL-based Pipeline vs. Native APICAMEL-based Pipeline vs. Native API
| Model | Framework | Pass@1 (%) | Pass@3 (%) | Pass@10 (%) |
| :--- | :--- | :---: | :---: | :---: |
| Qwen3-32B | Native ModelScope API | 50.0 | 57.1 | 71.4 |
| Qwen3-32B | **CAMEL-based Pipeline** | **60.7** | **64.3** | **82.1** |
| QwQ-32B-Preview | Native ModelScope API | 53.6 | 57.1 | 67.9 |
| QwQ-32B-Preview | **CAMEL-based Pipeline** | **67.9** | **71.4** | **78.6** |

#### Table 3. Terminal Bnech: Among all agents with same model, Claude Sonnet 4.5, our chat agent with terminal toolkit achieved top 5-run accuracy. 

| Agent           | Model              | Agent Org      | Model Org   | Accuracy            |
|-----------------|--------------------|----------------|-------------|---------------------|
| Ours            | Claude Sonnet 4.5  | Ours       | Anthropic   | 46.5% ± 2.4         |
| Goose           | Claude Sonnet 4.5  | Block          | Anthropic   | 43.1% ± 2.6         |
| Terminus 2      | Claude Sonnet 4.5  | Terminal Bench | Anthropic   | 42.8% ± 2.8         |
| OpenHands       | Claude Sonnet 4.5  | OpenHands      | Anthropic   | 42.6% ± 2.8         |
| Mini-SWE-Agent  | Claude Sonnet 4.5  | Princeton      | Anthropic   | 42.5% ± 2.8         |
| Claude Code     | Claude Sonnet 4.5  | Anthropic      | Anthropic   | 40.1% ± 2.9         |

## 2. LLM Judge Calibration

### 2.1 Rule-based Benchmarks

#### Table 4. Benchmarks with Rule-Based Evaluation Using Ground Truth

| Experiment Senario                                                         | Rule-based evaluation |
|--------------------------------------------------------------|------------|
| Long-Tail Question Answering (PopQA)                         | true       |
| Dual-Arm Robotic Manipulation (RoboTwin2.0)                  | true       |
| Tool-Agent-User Interaction (τ²-Bench)                       | true       |
| Terminal Operations (Terminal Bench)                         | true       |
| General Assistant (GAIA)                                     | true       |
| Multimodal tool use (M3-Bench)                               | true       |
| Reasoning Data Distillation                                  | true       |
| Autonomous Data Curation                                     | true       |
| Resolving GitHub Issues (SWE-Bench Verified)                 | true       |
| Collaborative Software Development (ChatDev reproduction)    | true       |
| Image Understanding (MMEBench)                               | true       |
| Simulating Population Decision Dynamics (MF-LLM / WEIBO)     | true       |
| Vulnerability Assessment (InjecAgent)                        | true       |
| Threat simulation (Chimera)                                  | true       |
| Interactive Medical Consultation                             | true       |

### 2.2 Agent as a Juedge

#### Table 5. Inter-rater reliability (Cohen's weighted kappa, quadratic) across four judge configurations on 1,550 aligned MT-Bench items. Interpretation follows [1]: >0.60 substantial, >0.40 moderate. （All judges evaluate 80 MT-Bench questions across 8 categories (coding, extraction, humanities, math, reasoning, roleplay, STEM, writing)）

| Judge Pair | Kappa (quad) | Interpretation |
|-----------|-------------|----------------|
| Ollama-20b ↔ CAMEL-120b | 0.740 | Substantial |
| CAMEL-20b ↔ CAMEL-120b | 0.697 | Substantial |
| GPT-4 (LLM) ↔ CAMEL-120b (Agent) | 0.691 | Substantial |
| Ollama-20b ↔ CAMEL-20b | 0.573 | Moderate |
| GPT-4 (LLM) ↔ Ollama-20b | 0.505 | Moderate |
| GPT-4 (LLM) ↔ CAMEL-20b (Agent) | 0.504 | Moderate |

[1] Landis JR, Koch GG. The measurement of observer agreement for categorical data. Biometrics. 1977 Mar;33(1):159-74. PMID: 843571.

#### Table 6. Model-level rank correlations (point-wise scoring, 31 models).
| Judge Pair | Spearman rho | Top-5 Overlap |
|-----------|-------------|---------------|
| GPT-4 ↔ CAMEL oss-120b | **0.974** | 5/5 (100%) |
| GPT-4 ↔ CAMEL oss-20b | 0.934 | 4/5 (80%) |
| CAMEL oss-20b ↔ CAMEL oss-120b | 0.926 | — |

#### Table 7. Category-level score bias (deviation from ensemble mean). 

| Category | GPT-4 (LLM) | Ollama-20b | CAMEL-20b (Agent) | CAMEL-120b (Agent) |
|----------|-------------|------------|-------------------|-------------------|
| Extraction | +0.65 | -0.61 | -0.01 | -0.02 |
| Humanities | +1.58 | -1.51 | -0.04 | -0.02 |
| Roleplay | +1.47 | -1.28 | -0.06 | -0.13 |
| STEM | +1.48 | -1.35 | -0.03 | -0.10 |
| Writing | +1.53 | -1.00 | -0.51 | -0.02 |

#### Table 8. Score Variance Analysis (31 models, 8 categories, 1,550 items).** This statistical summary quantifies the decision stability across four independent judge configurations (GPT-4, Ollama-20b, CAMEL-20b, and CAMEL-120b).

| Metric | Statistical Value |
| :--- | :--- |
| **Total Judged Items** | 1,550 |
| **Mean Per-item Variance** | 2.10 |
| **Median Per-item Variance** | 1.25 |
| **High-Consistency Samples (Variance < 2.0)** | **60.3%** |
| **Category-wise Variance Stability (Range)** | 1.87 – 2.27 |

### 2.3 Others

#### Table 9. Scholarly Video Abstract Generation: Human–LLM Agreement and Correlation (Three volunteers independently rated the final videos on four dimensions, with scores averaged across annotators. Agreement is computed for human-only evaluators and across LLM judges (GPT-4.1 and Gemini-3-Flash).)

| Evaluation Group                         | Agreement Score |
|------------------------------------------|-----------------|
| Human-only (Fleiss' Kappa)               | 0.72            |
| Human + GPT-4.1 (Fleiss' Kappa)          | 0.69            |
| GPT-4.1 vs Gemini-3-Flash (Spearman)     | 0.81            |
| GPT-4.1 vs GPT-4.1 (Spearman)            | 0.92            |


#### Table 10. Genetic Perturbation Analysis: Cross-Judge Consistency (Ten independently generated reports under the same query were evaluated by three LLM judges on a 0–5 scale. The table reports the mean ± std of interpretation scores across reports for each judge.)

|  | Gemini-2.5-flash | Sonnet 4.6 | Qwen 3.5 Plus |
| --- | --- | --- | --- |
| Interpretation Score | 4.875 ± 0.0625 | 3.6875 ± 0.1406 | 4.125 ± 0.0625 |


#### Table 11. Customizable Role-Playing: Pearson correlations and p-values between model scores and human annotations.
| Metric  | GPT-4.1           | DeepSeek-R1-0528 | DeepSeek-V3-0324 |
|---------|-------------------|------------------|------------------|
| CR      | 0.7075 (0.0000)   | 0.6285 (0.0000)  | 0.4875 (0.0024)  |
| FR      | 0.6630 (0.0000)   | 0.5788 (0.0002)  | 0.5995 (0.0001)  |
| RR      | 0.5602 (0.0002)   | 0.6304 (0.0000)  | 0.5937 (0.0001)  |
| CA      | 0.6174 (0.0000)   | 0.6103 (0.0000)  | 0.4296 (0.0044)  |
| PA      | 0.5877 (0.0002)   | 0.4677 (0.0073)  | 0.4346 (0.0153)  |
| Average | 0.6275 (0.0000)   | 0.5808 (0.0000)  | 0.4982 (0.0000)  |

## 3. Large Scale Experiments

#### Table 12. Latency (seconds) under different request volumes and concurrency settings

| Request Volume | 10 | 100 | 1K | 10K | 100K | 1M |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 20 threading, 1 port* | 10.34s | 9.79s | 19.24s | 112.00s | 1007.13s | — |
| 60 threading, 3 ports* | 10.72s | 11.70s | 12.36s | 43.02s | 352.97s | — |
| 80 threading, 10 ports* | 16.01s | 12.95s | 27.91s | 47.65s | 273.19s | — |
| 200 threading, 10 ports* | 15.65s | 22.90s | 15.74s | 57.62s | 146.14s | — |
| 320 threading, 10 ports* | 19.92s | 27.35s | 20.46s | 43.56s | 104.53s | — |
| **Ours** | **6.38s** | **6.79s** | **7.18s** | **9.17s** | **13.50s** | **29.59s** |

*\* Denotes our reproduction from OASIS.*