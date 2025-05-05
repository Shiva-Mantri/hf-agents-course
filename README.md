# Hugging Face Agents Course

## General Information
* **Course**: https://huggingface.co/learn/agents-course (source for notes below)
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
Messages/input to LLM model must be formatted into a specific string format. We use chat templates to bridge between conversational messages (user and assistant turns) and the specific formatting requirements.  

#### Messages
**System messages** (also called System Prompts) define how the model should behave. Define a role and content. e.g. Polite response vs Rude response. When using Agents, we list available tools as well.
```
system_message = {
    "role": "system",
    "content": "You are a professional customer service agent. Always be polite, clear, and helpful."
}
```

**Conversations: User and Assistant Messages** Chat templates help maintain context, by preserving conversation history, storing previous exchanges between user and assistant.
```
conversation = [
    {"role": "user", "content": "I need help with my order"},
    {"role": "assistant", "content": "I'd be happy to help. Could you provide your order number?"},
    {"role": "user", "content": "It's ORDER-123"},
]
```

**Chat Template** will format this into a Prompt that model would understand e.g. like `<|im_start|>` etc.
```
<|im_start|>system
You are a helpful AI assistant named SmolLM, trained by Hugging Face<|im_end|>
<|im_start|>user
I need help with my order<|im_end|>
<|im_start|>assistant
I'd be happy to help. Could you provide your order number?<|im_end|>
<|im_start|>user
It's ORDER-123<|im_end|>
<|im_start|>assistant
```

**Base Models** are trainined on raw text data to predict next token.  

**Instruct Models** are fine-tuned specifically to follow instructions and engage in conversations.  
e.g. `SmolLM2-135M` is base model, and `SmolLM2-135M-Instruct` is its instruction tuned variant.

**Applying Chat Template**
The rendered prompt can be used as input to model that we chose.
```
from transformers import AutoTokenizer

tokenizer = AutoTokenizer.from_pretrained("HuggingFaceTB/SmolLM2-1.7B-Instruct")
rendered_prompt = tokenizer.apply_chat_template(messages, tokenize=False, add_generation_prompt=True)
```
