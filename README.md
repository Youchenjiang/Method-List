# Method List - A Knowledge Base of Technical Methods and Solutions

[閱讀繁體中文版](README.zh-TW.md)

[![GitHub](https://img.shields.io/badge/GitHub-Method--List-blue)](https://github.com/Youchenjiang/Method-List)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

> A comprehensive knowledge base that collects technical tutorials, tool resources, and problem-solving solutions.

## Table of Contents

- [Method List - A Knowledge Base of Technical Methods and Solutions](#method-list---a-knowledge-base-of-technical-methods-and-solutions)
  - [Table of Contents](#table-of-contents)
  - [Introduction](#introduction)
  - [Folder Structure](#folder-structure)
  - [Content Overview](#content-overview)
    - [📚 Topics](#-topics)
    - [🗂️ Resources](#️-resources)
  - [Contribution Guidelines](#contribution-guidelines)
  - [Contact](#contact)
  - [License](#license)

## Introduction

Method List is a knowledge base dedicated to collecting and organizing technical methods, tool resources, and problem-solving solutions. It aims to provide a convenient platform for developers, tech enthusiasts, and learners to find and learn resources.

## Folder Structure

```tree
Method-List/
├── README.md
├── resources/
│   ├── agent-rules/     # AI agent behavior rules (copy-paste into CLAUDE.md / AGENTS.md)
│   ├── media/          # Media channels and collections
│   ├── online/         # Web tools and services
│   ├── software/       # Software recommendations
│   ├── system-prompts/ # AI assistant prompt templates
│   ├── tools/          # Command references and shortcuts
│   └── github/         # GitHub repository references
└── topics/
    ├── ai/             # AI and machine learning
    │   └── machine-learning/  # ML assignments, paper reviews, feature selection
    ├── android/        # Android security & automated testing architecture
    │   └── pentest/    # Android LLM-augmented pentesting framework (01-07)
    ├── data-engineering/ # Data engineering concepts
    ├── development/    # Development troubleshooting & SOPs
    ├── mindset/        # Personal mindset and reflection
    ├── quantum/        # Quantum computing research
    ├── research-method/ # Research methodology course notes & exam prep
    ├── security/       # Information security & ops cheatsheets
    └── technology/     # Hardware and software Q&A
```

## Content Overview

This knowledge base is divided into two main sections:

### 📚 Topics

In-depth technical articles, tutorials, and problem-solving solutions organized by domain:

- **AI** ([topics/ai/](topics/ai/)) - Artificial intelligence, machine learning, Azure OpenAI
  - **Machine Learning** ([topics/ai/machine-learning/](topics/ai/machine-learning/)) - ML assignments, paper reviews (AutoVulnPHP, STAF), and feature selection research → [Details](topics/ai/machine-learning/README.md)
- **Android** ([topics/android/](topics/android/)) - Android mobile security & automated analysis
  - **Augmented Pentesting Framework** ([topics/android/pentest/](topics/android/pentest/)) - 7-part architecture combining LLM, Agentic workflows, and Frida instrumentation → [Details](topics/android/pentest/README.md)
- **Data Engineering** ([topics/data-engineering/](topics/data-engineering/)) - Data processing and engineering concepts
- **Development** ([topics/development/](topics/development/)) - Programming troubleshooting, Docker, Git, and Conda environment SOPs
- **Mindset** ([topics/mindset/](topics/mindset/)) - Personal mindset and reflection
- **Quantum** ([topics/quantum/](topics/quantum/)) - Quantum computing research
- **Research Methods** ([topics/research-method/](topics/research-method/)) - Research methodology complete course notes (Lectures 01-08) & exam prep (NCU) → [Details](topics/research-method/README.md)
- **Security** ([topics/security/](topics/security/)) - Information security concepts, lab platforms, and ops cheatsheets → [Details](topics/security/README.md)
  - **Labs & Platforms** ([topics/security/cybersecurity-labs-and-platforms.md](topics/security/cybersecurity-labs-and-platforms.md)) - TryHackMe, HTB, DVWA, Vulnhub online/local labs
  - **CTF Beginner Guide** ([topics/security/ctf-beginner-guide.md](topics/security/ctf-beginner-guide.md)) - 6 core categories, 8 competition formats, and solution SOP
  - **Exam & Terminology Notes** ([topics/security/information-security-notes.md](topics/security/information-security-notes.md)) - Auth protocols (OAuth/SAML/OIDC), AAA, and high-frequency exam points
  - **Ops Cheatsheet** ([topics/security/network-security-cheatsheet.md](topics/security/network-security-cheatsheet.md)) - Nmap scanning, Wireshark/tcpdump filtering, and firewall rules
  - **Automation Security Analysis** ([topics/security/automation-analysis-logic.md](topics/security/automation-analysis-logic.md)) - Phase 1 intent analysis and taint tracking logic
  - **PDF Standard Encryption Cracking** ([topics/security/pdf-encryption-cracking.md](topics/security/pdf-encryption-cracking.md)) - Key derivation algorithms, MD5+RC4 cryptanalysis, and multiprocessing cracking
  - **Web Security Assessment Workflow** ([topics/security/web-application-security-assessment.md](topics/security/web-application-security-assessment.md)) - End-to-end security assessment methodology (Recon, Auth, API Fuzzing, TLS Review)
- **Technology** ([topics/technology/](topics/technology/)) - Hardware and software Q&A

### 🗂️ Resources

Curated collections of tools, software, media, and reference materials:

- **Agent Rules** ([resources/agent-rules/](resources/agent-rules/)) - Reusable behavior rules for AI agents. Copy-paste into your CLAUDE.md / AGENTS.md to improve agent problem-solving.
- **Media** ([resources/media/](resources/media/)) - YouTube channels, music, and video collections
- **Online** ([resources/online/](resources/online/)) - Web-based tools and services
- **Software** ([resources/software/](resources/software/)) - Computer and mobile app recommendations
- **System Prompts** ([resources/system-prompts/](resources/system-prompts/)) - AI assistant prompt templates (例如 `data-organization-expert_profiles.md`，單檔整合 Storyline/Deep Dive/Third-Person 三種 Profile 與 Turbo 模組) → [Details](resources/system-prompts/)
- **Tools** ([resources/tools/](resources/tools/)) - Command references, shortcuts, and **quick-fix commands** → [Details](resources/tools/)
- **GitHub References** ([resources/github/](resources/github/)) - Curated list of valuable GitHub repositories

## Contribution Guidelines

Contributions to this knowledge base are welcome! Please refer to the existing category structure, place your document in the `topics` or `resources` folder, and submit a Pull Request.

## Contact

If you have any questions or suggestions, feel free to raise them via [GitHub Issues](https://github.com/Youchenjiang/Method-List/issues).

## License

This project is licensed under the [MIT License](LICENSE). You are welcome to use and share it freely.

---

If this project is helpful to you, please give it a Star!