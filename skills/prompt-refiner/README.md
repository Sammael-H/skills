# Prompt Refiner Skill

A high-end prompt engineering and optimization skill that transforms raw or messy prompts into concise, token-efficient, high-performance master prompts for systems like GPT, Claude, and Gemini.

## Overview

**prompt-refiner** is a meta-skill designed to help you:

- **Optimize existing prompts** – Make them more concise and token-efficient
- **Design new prompts** – Create structured, robust prompts from scratch
- **Specialize prompts** – Target specific domains (agentic workflows, skill definitions, MCP tools)
- **Reduce hallucinations** – Add guardrails and evaluation criteria

## When to Use

Use this skill when you want to:

- Improve or compress a prompt for GPT, Claude, Gemini, or another LLM
- Design a system prompt for a specialized agent
- Optimize a skill definition for Claude Code
- Create an MCP tool prompt
- Reduce token usage while maintaining quality

## Core Framework: PCTCE+O

Every optimized prompt follows these six pillars:

1. **Persona** – Define the role and expertise the AI should adopt
2. **Context** – Include only necessary, material background information
3. **Task** – Use clear action verbs and define success criteria
4. **Constraints** – Specify output format, things to avoid, and limits
5. **Evaluation** – Add self-check instructions for the target AI
6. **Optimization** – Aggressively remove redundancy and compress language

## Domain Specialization Patterns

The skill includes three specialized patterns:

### 1. Agentic Prompts
For agent workflows with tool declarations, routing logic, state management, error handling, and termination conditions.

### 2. Skill Definitions
For reusable Claude Code skills with YAML frontmatter, role definition, available actions, workflow, error handling, and composition.

### 3. MCP Tool Prompts
For Model Context Protocol tool design with input/output schemas, error codes, rate limits, and integration notes.

## Output Format

All optimizations follow a strict, four-part format:

1. **🎯 Target AI & Mode** – Specify the intended model and style
2. **⚡ Optimized Request** – The final, copy-paste-ready prompt
3. **🛠 Applied Techniques** – List techniques used and token measurements
4. **🔍 Improvement Questions** – Suggest refinements for future iterations

## Usage Example

```
Use /prompt-refiner to optimize this raw prompt:
"I want an agent that searches for companies and analyzes them. It should use web search, 
company database lookup, and financial analysis. Make it work fast and handle errors well."
```

The skill will return a structured, optimized agentic prompt with:
- Clear tool declarations
- Routing logic
- State management
- Error handling
- Termination conditions
- Token count estimation

## Token Efficiency

The skill measures and reports:
- Original token count
- Optimized token count
- Percentage savings
- Domain-specific overhead (for agentic/specialized prompts)

## Safety & Hallucination Control

Every optimized prompt includes:
- Instructions for the target AI to admit uncertainty
- Guidance to avoid fabricating statistics or URLs
- Emphasis on evidence-based reasoning
- Clear assumptions and qualifications

## Related Skills

- **skill-creator** – Create new Claude Code skills from scratch
- **mcp-builder** – Design and build MCP tools
- **webapp-testing** – Test and validate optimized prompts in production
