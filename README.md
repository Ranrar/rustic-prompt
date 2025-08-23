# 🦀 Rustic Prompt
A collection of AI instruction files designed specifically for **Rust developers**.  
Use these instructions to power intelligent agents in tools like **GitHub Copilot**, **VS Code**, or any AI-powered development assistant.

- **Instruction sets** – predefined prompts and role definitions for Rust-related tasks.  
- **Agent behavior files** – configurations for AI agents to act as Rust coding assistants.  

They are tailored for building intelligent Rust developer tools and agents, and are ideal for integration with **Copilot**, **LLMs**, and **AI-enhanced developer workflows**.


| Title | Description | Open in VS Code |
| ----- | ----------- | --------------- |
| **Rust Code Instructions** | Agent guidance for handling Rust-specific coding workflows. | [![Open in VS Code](https://img.shields.io/badge/Open%20in-VS%20Code-007ACC?style=flat-square&logo=visualstudiocode&logoColor=white)](https://vscode.dev/github/Ranrar/rustic-prompt/blob/main/.github/instructions/rust/rust.instructions.md) |
| **Lint Specialist** | Analyze Rust lints, trace code interactions, and resolve false positives. Enhanced with trace analysis. | [![Open in VS Code](https://img.shields.io/badge/Open%20in-VS%20Code-007ACC?style=flat-square&logo=visualstudiocode&logoColor=white)](https://vscode.dev/github/Ranrar/rustic-prompt/blob/main/.github/instructions/rust/linthunter.instructions.md) |
| **Pest** or **PEGs** | Instructions and examples for working with the Pest parser in Rust. | [![Open in VS Code](https://img.shields.io/badge/Open%20in-VS%20Code-007ACC?style=flat-square&logo=visualstudiocode&logoColor=white)](https://vscode.dev/github/Ranrar/rustic-prompt/blob/main/.github/instructions/rust/pest.instructions.md) |
| **RON** | Instructions and examples for working with RON (Rusty Object Notation) in Rust. | [![Open in VS Code](https://img.shields.io/badge/Open%20in-VS%20Code-007ACC?style=flat-square&logo=visualstudiocode&logoColor=white)](https://vscode.dev/github/Ranrar/rustic-prompt/blob/main/.github/instructions/rust/ron.instructions.md) |

## General-Purpose Instructions
These instructions are designed for **any programming language or workflow** and can be used universally in VS Code or other AI-powered tools:

| Title | Description | Open in VS Code |
| ----- | ----------- | --------------- |
| **Syntax Error** | Diagnose and explain syntax errors in multiple languages. Clear and practical fixes. | [![Open in VS Code](https://img.shields.io/badge/Open%20in-VS%20Code-007ACC?style=flat-square&logo=visualstudiocode&logoColor=white)](https://vscode.dev/github/Ranrar/rustic-prompt/blob/main/.github/instructions/general/syntaxhunter.instructions.md) |
| **Debug Helper** | Structured debugging guide for agents to systematically resolve application bugs. | [![Open in VS Code](https://img.shields.io/badge/Open%20in-VS%20Code-007ACC?style=flat-square&logo=visualstudiocode&logoColor=white)](https://vscode.dev/github/Ranrar/rustic-prompt/blob/main/.github/instructions/general/debug.instructions.md) |

**Note:** Any AI model can be used with these files — either as **instructions** or in a **chat mode**, depending on your setup.

## Using in VS Code

You can use these files in **two ways** inside VS Code:  
1. As **Custom Instructions** (persistent behavior)  
2. As **Chat Mode** (temporary session guidance)  

### 1. Instructions Mode (Persistent)
This mode makes Copilot always follow the rules from a file.  
Good for consistent guidance, e.g., enforcing Rust formatting or coding standards.

Steps:
1. Open VS Code.  
2. Go to **Settings → GitHub Copilot → Configure Custom Instructions**.  
3. Copy the content of an instruction file (e.g., `instructions/rust_refactor.md`).  
4. Paste it into the **Custom Instructions** field.  
5. Save and restart Copilot.  

Now, every Copilot suggestion will be shaped by the Rust-specific instructions.

### 2. Chat Mode (Session-Based)
This mode applies the file only for one chat session.  
Good for **ad-hoc tasks**, e.g., refactoring one module or debugging a function.

Steps:
1. Open the **Copilot Chat** panel (`Ctrl+Shift+I` / `Cmd+Shift+I`).  
2. Paste the content of an instruction file as your **first message**.  
3. Continue the conversation — the assistant will follow those rules until the chat resets.  

### Key Difference

| Mode              | When to Use                              | Scope                        |
|-------------------|-------------------------------------------|------------------------------|
| **Instructions**  | Long-term guidance (always on)           | Persistent across sessions   |
| **Chat Mode**     | Short-term, task-specific instructions   | Only active in one chat      |

Tip: Combine both — set **general Rust coding rules** in Instructions Mode, and use **Chat Mode** for specific workflows like migrations, refactors, or testing.

## Credits

This project draws inspiration from prominent AI prompt collections and experts in the developer community:

| Name   | Description                                                                            | Link                                                                                                                           |
| ------------- | -------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------ |
| burkeholland  | Curated AI prompt examples and developer workflows, widely used for improving coding productivity. | [Links](https://gist.github.com/burkeholland) |
| voidfnc       | A collection of advanced AI prompts designed to enhance coding assistants and automation. | [Links](https://github.com/voidfnc/voidfnc_prompts) |


## Other AI Prompts

Discover these valuable prompt repositories and resources for AI-assisted development:

| Name                            | Description                                                               | Link                                                                                                                         |
| ------------------------------- | ------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------- |
| Beastmode Chatmode by burkeholland | Powerful chat-based AI prompts for enhanced interaction and code generation workflows. | [Links](https://gist.github.com/burkeholland/88af0249c4b6aff3820bf37898c8bacf#file-beastmode-chatmode-md) |
| voidfnc Prompts Repo            | Diverse prompt templates aimed at improving AI coding helpers and LLM responses. | [Links](https://github.com/voidfnc/voidfnc_prompts) |
| GitHub Awesome Copilot          | Community-curated list of tools, prompts, and tips to boost GitHub Copilot usage. | [Links](https://github.com/github/awesome-copilot) |
| System Prompts by x1xhlol       | Collection of system-level AI prompts and models for customizing AI assistants. | [Links](https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools) |
| TaskSync by 4regab              | AI-driven task management prompts designed to synchronize workflows and productivity. | [Links](https://github.com/4regab/TaskSync/) |

## Create Your Own

Master the art of prompt engineering with this comprehensive guide:

| Name | Description | Link |
| ----- | ----------- | ---- |
| Guide | Official OpenAI guide detailing best practices for crafting effective prompts. | [Links](https://cookbook.openai.com/) |
