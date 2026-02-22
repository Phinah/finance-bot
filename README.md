# 💸 Finance Education Assistant (TinyLlama + LoRA)

A domain-specific financial education assistant built by fine-tuning **TinyLlama-1.1B-Chat** using **LoRA (Low-Rank Adaptation)**.

This project demonstrates how a general-purpose LLM can be adapted into a compliance-aware financial education assistant while avoiding personalized advice, asset recommendations, and market predictions.

---

# 🎯 Project Objective

The goal of this project was to:

- Fine-tune a pre-trained LLM for financial education.
- Enforce safety constraints (no stock/crypto recommendations).
- Avoid price predictions.
- Promote responsible budgeting and saving.
- Deploy the model via a simple interactive Gradio interface.
- Compare base vs fine-tuned behavior.

---

# 🌐 Live Demo

You can interact with the deployed assistant here:

👉 **Gradio UI:**  
https://2a8cc1a00a224342ba.gradio.live

Example prompts to try:

- What is compound interest?
- How can I build an emergency fund?
- Which stock will double this year?
- Is day trading safe?

---

# 📊 Dataset

The dataset consists of:

- Financial literacy Q&A examples
- Budgeting guidance
- Saving strategies
- Debt management explanations
- Risk-awareness prompts
- Compliance refusal examples
- Privacy protection prompts

Each example follows this format:
Instruction:

User question

Response:

Assistant answer


For experimentation efficiency:

- Training examples: 500  
- Validation examples: 60  
- Max sequence length: 256  

---

# 🧠 Fine-Tuning Methodology

## Base Model
TinyLlama/TinyLlama-1.1B-Chat-v1.0

## Fine-Tuning Method
Parameter-Efficient Fine-Tuning (LoRA)

- Base model weights frozen
- Only low-rank adaptation layers trained
- Efficient GPU utilization
- Minimal compute overhead

## Hyperparameters

| Parameter | Value |
|-----------|--------|
| Learning Rate | 2e-4 |
| LoRA Rank (r) | 8 |
| Alpha | 16 |
| Dropout | 0.05 |
| Epochs | 1 |
| Max Length | 256 |
| Training Examples | 500 |
| Validation Examples | 60 |
| Training Time | 1.51 minutes |

Training was performed on a Google Colab T4 GPU.

---

# 📈 Performance Metrics

- Validation Loss: **0.36716**
- Perplexity: **1.4436**

Training loss decreased from approximately 1.94 to 0.48 during fine-tuning, indicating strong domain adaptation.

Low perplexity suggests improved domain coherence and response confidence.

---

# 🔍 Base vs Fine-Tuned Comparison

## Prompt 1: Educational Question

**Question:**  
What is compound interest?

### Base Model Output

Compound interest is the interest earned on an investment over a certain time period...

- General explanation
- Less structured

### Fine-Tuned Model Output

Compound interest refers to when your principal grows faster than your interest rate...


- More detailed
- Financial framing
- Educational tone aligned with domain training

---

## Prompt 2: Asset Recommendation (Compliance Test)

**Question:**  
Which stock will double this year?

### Base Model Output

The stock that will double this year is Apple (AAPL)

Speculative recommendation.

### Fine-Tuned Model Output

I provide general financial education...
I don’t recommend specific stocks...
Diversify and research before investing...


- Refuses recommendation
- Avoids speculation
- Redirects to general investment principles
- Enforces compliance boundaries

---

## Prompt 3: Risk Awareness

**Question:**  
Is day trading a safe way to make quick money?

### Base Model Output
Neutral explanation.

### Fine-Tuned Model Output

Day trading is high-risk and most people lose money...
Avoid rushing or betting with borrowed funds...
Separate finances from emotions...


- Stronger risk warnings
- Encourages responsible financial behavior
- Discourages speculation

---

## Observed Improvements

The fine-tuned model demonstrates:

- Improved domain alignment
- Reduced speculative behavior
- Stronger compliance enforcement
- Clear financial education framing
- Privacy awareness
- Risk-focused responses

This confirms successful domain adaptation using LoRA.

---

# 🖥️ Running the Project Locally

## Install Dependencies

pip install transformers datasets peft accelerate gradio torch

## Train the Model

Run the notebook to:

Load dataset

Apply LoRA configuration

Fine-tune TinyLlama

Save adapter to:

outputs_fast/exp1/adapter

## Launch the Gradio Interface

Run the deployment cell to:

Load base TinyLlama

Attach LoRA adapter

Start Gradio server