# 🦀 Rustic Prompt

A collection of AI instruction files designed specifically for Rust developers. Use these instructions to power intelligent agents in tools like **GitHub Copilot**, **VS Code**, or any AI-powered development assistant.

## Instruction Files
This repository contains instruction sets and agent behavior files tailored for building intelligent Rust developer tools and agents. Ideal for integrating with Copilot, LLMs, and AI-enhanced developer workflows.


| Title | Description | Open in VS Code |
| ----- | ----------- | --------------- |
| **Rust Specific Instructions** | Agent guidance for handling Rust-specific coding workflows. | [![Open in VS Code](https://img.shields.io/badge/Open%20in-VS%20Code-007ACC?style=flat-square&logo=visualstudiocode&logoColor=white)](https://vscode.dev/github/Ranrar/rustic-promt/blob/main/.github/instructions/rust.instructions.md) |
| **Rust Lint Specialist** | Analyze Rust lints, trace code interactions, and resolve false positives. Enhanced with trace analysis. | [![Open in VS Code](https://img.shields.io/badge/Open%20in-VS%20Code-007ACC?style=flat-square&logo=visualstudiocode&logoColor=white)](https://vscode.dev/github/Ranrar/rustic-promt/blob/main/.github/instructions/linthunter.instructions.md) |
| **Syntax Error Specialist** | Diagnose and explain syntax errors in multiple languages. Clear and practical fixes. | [![Open in VS Code](https://img.shields.io/badge/Open%20in-VS%20Code-007ACC?style=flat-square&logo=visualstudiocode&logoColor=white)](https://vscode.dev/github/Ranrar/rustic-promt/blob/main/.github/instructions/syntaxhunter.instructions.md) |
| **Debug Mode Instructions** | Structured debugging guide for agents to systematically resolve application bugs. | [![Open in VS Code](https://img.shields.io/badge/Open%20in-VS%20Code-007ACC?style=flat-square&logo=visualstudiocode&logoColor=white)](https://vscode.dev/github/Ranrar/rustic-promt/blob/main/.github/instructions/debug.instructions.md) |

## About This Project

The goal of this repo is to support **intelligent Rust tooling** by embedding AI instruction sets tailored to key developer tasks like linting, syntax correction, and debugging.

Each file in `.github/instructions/` can be referenced by AI agents, Copilot extensions, or automation tools to provide context-aware support.

## Directory Structure

```
📦 rustic-promt/
└── .github/
└── instructions/
├── rust.instructions.md
├── linthunter.instructions.md
├── syntaxhunter.instructions.md
└── debug.instructions.md
```

## How To Use

> **Usage:**  
> Copy any of the provided instruction files into your own project's `.github/instructions` directory.  
> You can then reference them in your AI tools, Copilot agents, or developer assistant setups.

## Contribute

Feel free to test-drive the various instruction sets and provide feedback by opening an issue — or make a pull request if you have improvements!

## Credits

Inspired by:

- [burkeholland](https://gist.github.com/burkeholland)  
- [voidfnc](https://github.com/voidfnc/voidfnc_prompts)

## Other AI Prompts

- https://gist.github.com/burkeholland/88af0249c4b6aff3820bf37898c8bacf#file-beastmode-chatmode-md  
- https://github.com/voidfnc/voidfnc_prompts  
- https://github.com/github/awesome-copilot  
- https://github.com/x1xhlol/system-prompts-and-models-of-ai-tools  
- https://github.com/4regab/TaskSync/

## Create Your Own

- https://cookbook.openai.com/examples/gpt4-1_prompting_guide
