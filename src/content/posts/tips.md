---
author: David Howard
pubDate: 2025-07-01
title: Tips For LLM Coders
postSlug: llm-coder-tips
featured: true
draft: false
tags:
  - LLM
  - Coders
  - AI
description: 'A few tips to improve your LLM coding results.'
---

# Tips for LLM Coders

Here are a few practical tips for effectively working with Large Language Models (LLMs) to improve your code productivity and results.

## Prompt Engineering

### Write and Save Your Prompts

- Always write and save your prompts in a text file first
  - Lets you review and iterate until it looks good
  - Avoids submitting typos to the LLM
  - Allows you to rollback to previous versions
  - Enables easy sharing and reuse
  - If you need to modify a prompt:
    - Make a copy (in the same file) of the original prompt and modify the copy
    - This lets you see the progression and evolution of your prompts
    - Use clear naming or versioning (e.g., "v1", "v2", or timestamps)

### Use Structured Formats

- Write your prompts using either JSON or XML for complex requests
  - Makes delimiters clear and easy to parse
  - XML is often preferred for complex structured data and nested content
  - JSON works well for simple key-value pairs and lists
  - Always tell the LLM which format to use in its response
  - Example: "Please respond in XML format with clear section tags"

### Iterative Prompt Development

- Use an LLM to generate and improve your prompts
  - Instead of trying to write a detailed prompt from scratch, write a simpler prompt that calls out high-level requirements
  - Ask your LLM to generate a detailed, step-by-step process
  - Revise the prompt iteratively until it's perfect
  - Test with edge cases and different scenarios

## Version Control and Workflow

### Use Git for Checkpoints

- Create frequent git commits as you generate code or content
  - As you generate code (or other text) and it looks acceptable, commit it to git
  - Makes rollback easy if something goes wrong
  - Use descriptive commit messages like "feat: add user authentication logic"
  - Consider using conventional commit formats for consistency
  - Create branches for experimental changes

## Quality Assurance

### Multi-LLM Code Review

- Review your code with a different LLM than the one that generated it
  - Each LLM has different strengths and sees things differently
  - Use a different LLM to review your code for fresh perspective
  - Ask it for bullet points for each finding and use that as a checklist
  - Focus review on:
    - Correctness and logic
    - Performance and efficiency
    - Idiomatic code patterns
    - Security vulnerabilities
    - Documentation and readability

## Best Practices Summary

- Start simple, then iterate and refine
- Document your process and save your work
- Use multiple LLMs for different perspectives
- Leverage version control for safe experimentation
- Structure your inputs and outputs clearly
- Always review and validate generated content

## For more tips, check out this video:

- [Master Claude Code in 15 Minutes](https://www.youtube.com/watch?v=cjW6ofe7AY4)
