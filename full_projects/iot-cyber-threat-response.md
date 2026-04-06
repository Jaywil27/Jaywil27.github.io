---
layout: page
title: "Improving IoT Cyber Threat Response with Multi-Agent LLMs and Semantic Retrieval"
permalink: /full_projects/iot-threat-response/
---

Hello all, This is a project that was recently created and submitted to and presented at a IEEE conference in Sydney Australia.
https://doi.org/10.1109/SmartIoT66867.2025.00067

---

# Improving IoT Cyber Threat Response with Multi-Agent LLMs and Semantic Retrieval
---
## Project Overview

IoT environments are complex, heterogeneous, and often exposed to novel threats. Traditional LLM-based systems struggle with hallucinations and outdated knowledge, posing serious security risks.

This project introduces a multi-agent RAG (Retrieval-Augmented Generation) framework designed to address these challenges by:

- Decomposing complex security queries into actionable sub-questions  
- Retrieving evidence from structured (MITRE ATT&CK, IoT threat taxonomies) and unstructured sources  
- Synthesizing responses using specialized reasoning agents while reducing hallucinations  
- Using iterative feedback loops for verification, cross-validation, and contradiction resolution  

The architecture incorporates lightweight **LLaMA 3.2** for fast semantic tasks and **Mistral 7B** for deeper reasoning, combined with dense-vector and transformer-based retrieval methods.

---

## Framework Components

### 1. Decomposition Agent

- Breaks queries into sub-questions by device type, communication protocol, or threat category  
- Prevents prompt overload and ensures complete coverage of the problem space  

### 2. Goal Agent

- Interprets the broader intent of the user query  
- Converts loosely defined inputs into structured prompts for downstream agents  

### 3. Retrieval Agents

- Three parallel agents query both structured (MITRE ATT&CK) and unstructured sources  
- Improves recall, coverage, and reduces document overlap  

### 4. Debate Agent

- Cross-validates retrieved evidence  
- Detects contradictions and inconsistencies to improve trustworthiness  

### 5. Suggestion Agent

- Synthesizes the final output  
- Integrates evidence from prior agents  
- Minimizes hallucinations and verifies factual accuracy  

---

## Features

- Multi-agent orchestration for IoT cybersecurity reasoning  
- Semantic decomposition with targeted retrieval from MITRE ATT&CK and IoT datasets  
- Dynamic agent selection using vector-based similarity search  
- Feedback loops for improved reliability and context awareness  
- Compatible with both local and API-based LLM deployments  

---

## Setup and Usage

### Clone the repository

git clone https://github.com/Jaywil27/Improving-IoT-Cyber-Threat-Response.git
