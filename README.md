# Constraint-Based-Story-Generator
### *Fine-Tuned LLaMA-3.2-1B Model + Evaluation + Constraint Planning*

This repository contains a complete workflow for building a **hybrid neural–symbolic story generation system**. It integrates a **fine-tuned LLaMA-3.2-1B model**, narrative evaluation metrics, rule-based constraint enforcement, and an iterative “generate → evaluate → refine” pipeline.



## ** Repository Structure**

```
.
├── llama32_1b_outline_story/         # Original dataset or outline prompt set
├── llama32_1b_outline_trained/       # Final LoRA-trained LLaMA-3.2-1B model
│   ├── adapter_config.json
│   ├── adapter_model.safetensors
│   ├── special_tokens_map.json
│   ├── tokenizer.json
│   └── tokenizer_config.json
│
├── Fine_Tuning_and_Initial.ipynb     # Notebook for dataset prep and LoRA fine-tuning
├── Final_AI.ipynb                    # Complete hybrid story generator and evaluation system
├──mystery_result.json
├──romance_story_result.json
└── README.md                         # Documentation (this file)
```

---

## ** Project Overview**

Story generation models often produce creative narratives but struggle with:

* maintaining coherence
* tracking characters
* enforcing story constraints
* ensuring logical consistency

This project solves these problems by combining:

### **1. Neural Generation (LLaMA-3.2-1B, fine-tuned with LoRA)**

* Fine-tuned on a custom dataset of hierarchical story outlines.
* Produces structured, high-quality narrative text.
* Uses *inference only*—no need to fine-tune again.

### **2. Narrative Aesthetic Evaluation**

Implements automatic scoring modules:

* **Coherence Scoring**
* **Emotional Arc Analysis**
* **Character Consistency Checking**
* **Lexical Richness Measurement (TTR / MTLD)**
* Optional **Bayesian Narrative Quality Estimator**

### **3. Symbolic Rule-Based Constraint Planning**

A modular system that checks:

* forbidden events
* required plot points
* timeline consistency
* character-role rules
* structural constraints (e.g., 3-act or 5-beat pattern)

Violations trigger:

* regeneration
* local text edits
* or guided refinement prompts

### **4. Final Iterative Loop**

```
Neural Generation
        ↓
Aesthetic + Bayesian Evaluation
        ↓
Constraint Violation Detection
        ↓
Symbolic Repair OR Re-generation
        ↓
Final Refined Story Output
```

---

## ** Notebooks **

### **1. Fine_Tuning_and_Initial.ipynb**

This notebook includes:

* dataset loading
* preprocessing
* training LoRA adapters
* saving model checkpoints

When training is complete, the LoRA adapter is stored in:

```
llama32_1b_outline_trained/
```

### **2. Final_AI.ipynb**

This is the main execution notebook. It performs:

#### **Model Loading (Inference Only)**

Loads the pre-trained base model + your LoRA adapter:

```python
tokenizer = AutoTokenizer.from_pretrained(base_model)
model = AutoModelForCausalLM.from_pretrained(base_model)
model = PeftModel.from_pretrained(model, lora_path)
```

No fine-tuning is repeated.

#### **Modules Implemented**

* StoryGenerator class
* Aesthetic metric calculators
* Emotion trajectory extractor
* Character graph checker
* Constraint planner (rule-based)
* Hybrid reasoning loop

#### **Expected Outputs**

* Initial raw story
* Evaluation scores
* Rule violations
* Final corrected narrative

---

## ** How to Run the Project**

### **1. Clone the repository**

```bash
git clone https://github.com/<your-username>/<repo-name>.git
cd <repo-name>
```

### **2. Open `Final_AI.ipynb` in Google Colab**

Click:
**Open in Colab → Runtime → Run All**

### **3. Make sure your LLaMA weights are in Google Drive**

Place the folder:

```
llama32_1b_outline_trained/
```

inside:

```
/MyDrive/1B20EP/
```

Modify paths in notebook if needed.

---

## ** Model Details**

**Base model:**
`meta-llama/Llama-3.2-1B`

**Training method:**
PEFT LoRA adaptation (memory-efficient)

**Dataset:**
Custom outline-to-story corpus
(inside `llama32_1b_outline_story/`)

---


## ** Authors**

**Divyansh Srivastava (IIT Bhubaneswar)** and 
**Pankaj Upadhyay (IIT Bhubaneswar)**

---

