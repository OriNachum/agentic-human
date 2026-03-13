---
layout: post
title: "Workbench Development: A Structured Approach to Agentic Coding"
date: 2025-05-28
tags: [agentic-ai, developer-experience]
original_url: https://medium.com/@ori.nachum_22849/workbench-development-a-structured-approach-to-agentic-coding-06964f24c581
---

Today's LLM coding agents show impressive results in small scopes. Tools like Cursor are already valuable in accelerating repetitive development tasks, bootstrapping apps, and navigating files. But as the interaction grows — either through longer conversations or larger codebases — things start breaking down.

That's where Workbench Development comes in.

## The problem with free-form agentic coding

We've worked with and around agentic development tools for a while. They're promising, but quickly run into limitations:

- **Context & Attention:** The model can't keep everything in mind, and things drop.
- **Model Hallucination:** Generated code often misses critical details or invents APIs.
- **Codebase Contamination:** Inconsistent style, security gaps, and unreviewed logic creep in.
- **Architectural Erosion:** The bigger the project, the harder it is to maintain high-level structure.
- **Explainability Gap:** It becomes harder to understand why the model made certain changes.
- **Maintenance Overhead:** The resulting code needs real humans to debug, align, and integrate.

Most of these issues stem from one thing: we treat the model like a dev-in-the-loop, but without giving it a proper environment.

## What is Workbench Development?

Workbench Development is my proposal for a more structured, modular approach to agentic coding.

Instead of asking a model to operate across the entire codebase in one go, we scope it to a predefined folder — a reliable workbench — where it can run isolated tasks.

Each agent gets its own repo or folder. It works locally, with well-defined boundaries. From there, we build up using recursive agent decomposition, where:

- Top-level agents analyze business logic and plan changes
- Tasks are broken down into component-level steps
- Leaf agents (workbenches) handle isolated manipulation of scoped files
- The changes are integrated back up by the higher-level agents

This makes the system composable, reliable, and easier to reason about.

## Architecture

At the core, we implemented a Kubernetes-native service called Agentic Developer, using:

- An MCP Server (Model Context Protocol) to receive instructions
- A wrapper around OpenAI Codex and any Chat Completions API-compatible providers (like VLLM, Ollama, Bedrock)
- A Responses API Server to unify model interaction and enrich calls with additional tools
- A recursive agent team, each with access to:
  - Graph-based knowledge
  - Conversation memory
  - A deterministic execution environment

Each agent can call another, forming a graph of sub-agents working in parallel or sequentially.

## How it works

When a request arrives, the process looks like this:

1. An MCP request is received (repo URL, branch, folder, instruction).
2. The repository is cloned locally.
3. The agent performs environment analysis (e.g. detecting config files).
4. Codex processes the instruction.
5. The agent performs code manipulation locally.
6. The result is reported back.

Each agent reads its own config, history, and system instruction from its scoped folder, keeping behavior consistent.

## Why it matters

We've used Workbench Development to build agent chains that:

- Preserve clean architectures
- Avoid redundant reasoning or contamination across modules
- Enable swapping models or tools in specific layers
- Reduce hallucination risk by narrowing model scope

It's not a silver bullet, but it's a step toward using LLMs like real contributors in a system — instead of chatbots with shell access.

## Open Source

Both the Agentic Developer MCP and open-responses-server are MIT licensed and available for reuse.

You can run the system with OpenAI, Google, or Amazon model APIs. Integration is done via adapters and a simple key management layer.

Please add a star if you find this useful or want to support us:

- Agentic Developer MCP: [github.com/teabranch/agentic-developer-mcp](https://github.com/teabranch/agentic-developer-mcp)
- Serve OpenAI Responses API based on any Chat Completions API Provider: [github.com/teabranch/open-responses-server](https://github.com/teabranch/open-responses-server)

## Meet the team

We are TeaBranch — Danny Teller, Ori Nachum, Allen Jacobson.

We are engineers from Tipalti Inc., organized to share MIT licensed code to offer much-needed, simple, k8s native, enterprise-grade solutions.

## What's next

We're continuing to experiment with:

- More intelligent task decomposition
- Model-specific folder behavior (e.g. using different models for code gen vs. planning)
- Better observability and explainability per agent

If you're working on agentic tooling, we'd love to compare notes.
