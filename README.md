# TabBridge: Bridging Structure and Context for Accurate Table Reasoning

🏆 **Best Paper Award at the ACL 2026 Workshop SURGeLLM** 🏆 <br>
Paper Link : https://aclanthology.org/2026.surgellm-1.14/

## Abstract
> Table reasoning remains challenging for Large Language Models (LLMs) as it requires integrating structured tabular information with natural language questions. Previous SQL-based approaches rely on surface-level alignment between question keywords and column headers, often generating queries with spurious or missing column mappings. 
> We introduce TabBridge, a framework that incorporates both structural and contextual information for accurate table reasoning. TabBridge first generates a unified textual representation called Table Specification (TabSpec), preserving the structural information through row and column analysis. In order to ensure accuracy and consistency, we also employ a reconstruction-based evaluation mechanism to verify and refine the generated TabSpec. TabSpec is subsequently used to generate SQL aligned with the contextual intent of the question, enabling accurate interpretation of column semantics that are often overlooked by previous approaches.
> Across three public benchmarks, TabBridge shows consistent improvements over previous SQL-based methods, achieving 73.94\% accuracy on WikiTableQuestions (+5.3 pp over the previous state of the art). TabBridge also demonstrates robust performance across diverse LLM backbones, confirming its generalizability across model architectures.

## Method Overview

Our research focuses on improving LLM reasoning and QA performance over table data through:
<img width="4544" height="2736" alt="Figure2" src="https://github.com/user-attachments/assets/6d3720a0-eb87-49ea-aaf9-e0b9510672e8" />


## Installation & Setup

### 1. Environment Setup

```bash
# Create virtual environment (Python 3.9 recommended)
python3.9 -m venv env

# Install dependencies
pip install -r requirements.txt
```

### 2. API Configuration

Create a `.env` file in the project root:

```bash
OPENAI_API_KEY=your_openai_api_key_here
```

## Execution

```bash
python run_tabbridge.py
```

## Project Structure

```
TabBridge/
├── 📁 datasets/     # Dataset files
│   ├── wtq.jsonl    # WikiTableQuestions dataset (main)
│   └── wtq.json     # Alternative format
├── 📁 prompt/                                 # All prompt templates
│   ├── TabSpec_Generation.txt                  # Table Specification generation
│   ├── SQL_Reasoning.txt                       # SQL query generation
│   ├── TabSpec_row_analysis_evaluation.txt     # Direct TabSpec evaluation
│   ├── SQL_Evaluation.txt                      # SQL quality assessment
│   ├── 📁 TabSpec_feedback/         # TabSpec refinement prompts
│   │   ├── row_analysis_feedback.txt
│   │   ├── header_feedback.txt
│   │   └── structure_feedback.txt
│   ├── 📁 SQL_feedback/             # SQL refinement prompts
│   │   ├── appropriate_role.txt
│   │   ├── well_used_row_analysis.txt
│   │   ├── appropriate_data_type.txt
│   │   └── faithfulness.txt
│   └── 📁 Table_Generation/         # Table reconstruction prompts
│       ├── Schema_Extraction.txt
│       ├── Instruction_Extraction.txt
│       └── Table_Generation.txt
├── 📁 utils/                                       # Core utility modules
│   ├── preprocess.py                               # Data preprocessing utilities
│   ├── prompt_wtq.py                               # Prompt loading and management
│   ├── tabspec_row_analysis_evaluator.py           # Direct TabSpec evaluation
│   ├── tabspec_reconstruction_based_evaluator.py   # Reconstruction-based TabSpec evaluation
│   └── sql_evaluator.py                            # SQL quality evaluation
├── 📁 outputs/                   # Generated results (auto-created)
│   ├── 📁 subtables/             # Cached sub-table extractions
│   ├── 📁 tabspec_logs/          # TabSpec generation & evaluation logs
│   ├── 📁 sql_logs/              # SQL generation & execution logs
│   ├── wtq_results.jsonl         # Final results (JSON format)
│   └── wtq_results.csv           # Final results (CSV format)
├── run_tabbridge.py              # Main execution script
├── subtable_extractor_euclid.py  # Sub-table extraction logic
└── requirements.txt              # Python dependencies
```
