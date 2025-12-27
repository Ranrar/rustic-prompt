# 🦀 Rustic Prompt
A collection of AI instruction files designed specifically for **Rust developers**.  
Use these instructions to power intelligent agents in tools like **GitHub Copilot**, **VS Code**, or any AI-powered development assistant.

- **Instruction sets** - predefined prompts and role definitions for Rust-related tasks.  
- **Agent behavior files** - configurations for AI agents to act as Rust coding assistants.  

They are tailored for building intelligent Rust developer tools and agents, and are ideal for integration with **Copilot**, **LLMs**, and **AI-enhanced developer workflows**.

Below you'll find ready-to-use instruction packs (openable directly in VS Code) plus a small set of recommended VS Code extensions that pair nicely with these workflows.


| Title | Description | Open in VS Code |
| ----- | ----------- | --------------- |
| **Rust Code Instructions** | Agent guidance for handling Rust-specific coding workflows. | [![Open in VS Code](https://img.shields.io/badge/Open%20in-VS%20Code-007ACC?style=flat-square&logo=visualstudiocode&logoColor=white)](https://vscode.dev/github/Ranrar/rustic-prompt/blob/main/.github/instructions/rust/rust.instructions.md) |
| **Lint Specialist** | Analyze Rust lints, trace code interactions, and resolve false positives. Enhanced with trace analysis. | [![Open in VS Code](https://img.shields.io/badge/Open%20in-VS%20Code-007ACC?style=flat-square&logo=visualstudiocode&logoColor=white)](https://vscode.dev/github/Ranrar/rustic-prompt/blob/main/.github/instructions/rust/linthunter.instructions.md) |
| **Pest** or **PEGs** | Instructions and examples for working with the Pest parser in Rust. | [![Open in VS Code](https://img.shields.io/badge/Open%20in-VS%20Code-007ACC?style=flat-square&logo=visualstudiocode&logoColor=white)](https://vscode.dev/github/Ranrar/rustic-prompt/blob/main/.github/instructions/rust/pest.instructions.md) |
| **RON** | Instructions and examples for working with RON (Rusty Object Notation) in Rust. | [![Open in VS Code](https://img.shields.io/badge/Open%20in-VS%20Code-007ACC?style=flat-square&logo=visualstudiocode&logoColor=white)](https://vscode.dev/github/Ranrar/rustic-prompt/blob/main/.github/instructions/rust/ron.instructions.md) |

## Rust multi-agent

The **multi-agent** pack is a self-contained set of path-specific instructions that work together:

- Folder: `.github/instructions/rust/multi-agent`

| File | Purpose | Open in VS Code |
| ---- | ------- | --------------- |
| `index.instructions.md` | Router/index that helps pick the right specialist for the task. | [![Open in VS Code](https://img.shields.io/badge/Open%20in-VS%20Code-007ACC?style=flat-square&logo=visualstudiocode&logoColor=white)](https://vscode.dev/github/Ranrar/rustic-prompt/blob/main/.github/instructions/rust/multi-agent/index.instructions.md) |
| `rust-core.instructions.md` | Baseline Rust conventions + Cargo hygiene. | [![Open in VS Code](https://img.shields.io/badge/Open%20in-VS%20Code-007ACC?style=flat-square&logo=visualstudiocode&logoColor=white)](https://vscode.dev/github/Ranrar/rustic-prompt/blob/main/.github/instructions/rust/multi-agent/rust-core.instructions.md) |
| `linthunter.instructions.md` | Rust lint triage and false-positive investigation workflow. | [![Open in VS Code](https://img.shields.io/badge/Open%20in-VS%20Code-007ACC?style=flat-square&logo=visualstudiocode&logoColor=white)](https://vscode.dev/github/Ranrar/rustic-prompt/blob/main/.github/instructions/rust/multi-agent/linthunter.instructions.md) |
| `pestmate.instructions.md` | Pest grammar specialist for `.pest` grammars and PEG debugging. | [![Open in VS Code](https://img.shields.io/badge/Open%20in-VS%20Code-007ACC?style=flat-square&logo=visualstudiocode&logoColor=white)](https://vscode.dev/github/Ranrar/rustic-prompt/blob/main/.github/instructions/rust/multi-agent/pestmate.instructions.md) |
| `ron-guide.instructions.md` | RON (Rusty Object Notation) specialist for `.ron` and serde workflows. | [![Open in VS Code](https://img.shields.io/badge/Open%20in-VS%20Code-007ACC?style=flat-square&logo=visualstudiocode&logoColor=white)](https://vscode.dev/github/Ranrar/rustic-prompt/blob/main/.github/instructions/rust/multi-agent/ron-guide.instructions.md) |

### Recommended Rust Extensions (VS Code)

| Name | Description | Marketplace |
| ---- | ----------- | ----------- |
| **rust-analyzer** | Rust language support (LSP): completion, navigation, refactors, inlay hints, diagnostics, formatting, and more. | [![VS Code Marketplace](https://img.shields.io/badge/VS%20Code%20Marketplace-Install-007ACC?style=flat-square&logo=visualstudiocode&logoColor=white)](https://marketplace.visualstudio.com/items?itemName=rust-lang.rust-analyzer) |
| **Cargo** | Commands to add/remove dependencies via Cargo (planned deprecation once rust-analyzer covers `cargo add`/`cargo rm`). | [![VS Code Marketplace](https://img.shields.io/badge/VS%20Code%20Marketplace-Install-007ACC?style=flat-square&logo=visualstudiocode&logoColor=white)](https://marketplace.visualstudio.com/items?itemName=panicbit.cargo) |
| **Even Better TOML** | TOML language support backed by Taplo (validation, formatting, schema-aware completion). | [![VS Code Marketplace](https://img.shields.io/badge/VS%20Code%20Marketplace-Install-007ACC?style=flat-square&logo=visualstudiocode&logoColor=white)](https://marketplace.visualstudio.com/items?itemName=tamasfe.even-better-toml) |
| **Search crates.io** | Crate name suggestions / completion while editing `Cargo.toml` (uses crates.io search API). | [![VS Code Marketplace](https://img.shields.io/badge/VS%20Code%20Marketplace-Install-007ACC?style=flat-square&logo=visualstudiocode&logoColor=white)](https://marketplace.visualstudio.com/items?itemName=belfz.search-crates-io) |
| **Pest IDE Tools** | IDE support for Pest grammars via LSP (errors, rename, go-to, hover, completion, formatting). | [![VS Code Marketplace](https://img.shields.io/badge/VS%20Code%20Marketplace-Install-007ACC?style=flat-square&logo=visualstudiocode&logoColor=white)](https://marketplace.visualstudio.com/items?itemName=pest.pest-ide-tools) |
| **RON** | RON (Rusty Object Notation) syntax support for VS Code (TextMate grammar). | [![VS Code Marketplace](https://img.shields.io/badge/VS%20Code%20Marketplace-Install-007ACC?style=flat-square&logo=visualstudiocode&logoColor=white)](https://marketplace.visualstudio.com/items?itemName=made-by.ron) |

## General-Purpose Instructions
These instructions are designed for **any programming language or workflow** and can be used universally in VS Code or other AI-powered tools:

| Title | Description | Open in VS Code |
| ----- | ----------- | --------------- |
| **Syntax Error** | Diagnose and explain syntax errors in multiple languages. Clear and practical fixes. | [![Open in VS Code](https://img.shields.io/badge/Open%20in-VS%20Code-007ACC?style=flat-square&logo=visualstudiocode&logoColor=white)](https://vscode.dev/github/Ranrar/rustic-prompt/blob/main/.github/instructions/general/syntaxhunter.instructions.md) |
| **Debug Helper** | Structured debugging guide for agents to systematically resolve application bugs. | [![Open in VS Code](https://img.shields.io/badge/Open%20in-VS%20Code-007ACC?style=flat-square&logo=visualstudiocode&logoColor=white)](https://vscode.dev/github/Ranrar/rustic-prompt/blob/main/.github/instructions/general/debug.instructions.md) |
| **Text Hygiene (ASCII only)** | Prevent smart punctuation and invisible/problematic characters in docs/config (especially `.md` and `.github/*`). | [![Open in VS Code](https://img.shields.io/badge/Open%20in-VS%20Code-007ACC?style=flat-square&logo=visualstudiocode&logoColor=white)](https://vscode.dev/github/Ranrar/rustic-prompt/blob/main/.github/instructions/general/text-hygiene.instructions.md) |
| **GitHub Security** | Prevent leaking secrets (API keys/tokens), handle `.env` safely, and harden GitHub Actions and repo settings. | [![Open in VS Code](https://img.shields.io/badge/Open%20in-VS%20Code-007ACC?style=flat-square&logo=visualstudiocode&logoColor=white)](https://vscode.dev/github/Ranrar/rustic-prompt/blob/main/.github/instructions/general/security-github.instructions.md) |

### General-Purpose Extensions (VS Code)

| Name | Description | Marketplace |
| ---- | ----------- | ----------- |
| **Emoji Eraser** | Highlights emojis as diagnostics and helps remove them (per-emoji quick fix + bulk remove command). | [![VS Code Marketplace](https://img.shields.io/badge/VS%20Code%20Marketplace-Install-007ACC?style=flat-square&logo=visualstudiocode&logoColor=white)](https://marketplace.visualstudio.com/items?itemName=ranrar.emoji-detector) |
| **Gremlins tracker** | Reveals invisible / confusable Unicode characters (zero-width spaces, non-breaking spaces, etc.). | [![VS Code Marketplace](https://img.shields.io/badge/VS%20Code%20Marketplace-Install-007ACC?style=flat-square&logo=visualstudiocode&logoColor=white)](https://marketplace.visualstudio.com/items?itemName=nhoizey.gremlins) |

**Note:** Any AI model can be used with these files — either as **instructions** or in a **chat mode**, depending on your setup.

## Using in VS Code

You can use these files in **three ways** inside VS Code:  
1. As **Custom Instructions** (persistent behavior)  
2. As **Chat Mode** (temporary session guidance)  
3. As **Agents** (multi-step workflows)  



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

### 3. Agents (Multi-step workflows)

If you're using an **agent-style** workflow (where the assistant can plan, edit files, and iterate across multiple steps), these instruction files work especially well as a "role + rules" foundation.

Typical flow:
1. Open **Copilot Chat**.
2. Switch to an **Agent** / **Agent Mode** experience (if your Copilot version supports it).
3. Paste the content of one of the instruction files as your first message (or summarize it and link the file), then describe the goal.
4. Ask the agent to:
	- propose a short plan,
	- make small incremental edits,
	- and verify results (build/tests) before finishing.

This is great for tasks like: refactors, migrations, lint triage, parser work (Pest), or tightening docs/CI.

### Key Difference

| Mode              | When to Use                              | Scope                        |
|-------------------|-------------------------------------------|------------------------------|
| **Instructions**  | Long-term guidance (always on)           | Persistent across sessions   |
| **Chat Mode**     | Short-term, task-specific instructions   | Only active in one chat      |
| **Agents**        | Multi-step tasks (plan → edit → verify)  | Can span multiple steps/files |

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
