# Hugging Face Agents Course

## General Information
* **Course**: https://huggingface.co/learn/agents-course
* **Project Due Date**: July 1st 2025

## Workspace and Notes
### Code
```
Code\...\hf-agents-course
```

### Ollama local [link](https://huggingface.co/learn/agents-course/en/unit0/onboarding#step-5-running-models-locally-with-ollama-in-case-you-run-into-credit-limits)
Download from Ollama site - https://ollama.com/download  
Pull a model locally. Stored locally at <user_home>\.ollama  
Use `LiteLLMModel` in `smolagent` [link](https://huggingface.co/learn/agents-course/en/unit0/onboarding#step-5-running-models-locally-with-ollama-in-case-you-run-into-credit-limits:~:text=Use%20LiteLLMModel%20Instead%20of%20HfApiModel)
```
ollama pull qwen2:7b
```
Start Ollama in the background
```
ollama serve
```
Other commands
```
ollama list
ollama show <model_name>
```

## Unit 1 - Introduction to Agents

### Introduction
An AI model capable of **reason, planning and interacting with its environment**.  
An Agent has two parts: **Brain** - AI Model, **Body** - Capabilities and Tools. 

**Brain**: Handles reasoning and planning. Which actions to take based on the situation.  
**Body**: Everything an agent is equipped to do.  

Most common AI model used for Agents is an LLM. Takes text as input, and outputs text. 

### LLMs
LLMs can be **run locally** or **use cloud/API**, e.g. via HF Serverless Inference API.

