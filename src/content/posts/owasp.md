---
author: David Howard
pubDate: 2025-08-05
title: OWASP Scanner-LLM
postSlug: owasp
featured: true
draft: false
description: 'A project using an LLM to scan for OWASP vulnerabilties'
---

# Building an AI-Powered Security Scanner: From OWASP Documentation to Automated Code Review

The full how-to instructions for this project are in github at [owasp-scanner](https://github.com/dmh2000/owasp-scanner). The bulk of the work is done by Claude and a set of prompts. The only code are a couple of simple programs to test the scanner against.

As developers increasingly rely on LLMs for code generation and assistance, there's a growing need for automated security review tools that can keep pace with rapid development cycles. This post explores how to build a comprehensive security scanning system using Claude Code, combining web scraping, documentation generation, and AI-powered vulnerability detection.

## The Challenge: Keeping Security Reviews Current

The [OWASP Top 10](https://owasp.org/www-project-top-ten/), while authoritative, exists primarily as web documentation rather than structured data that LLMs can efficiently consume. This project bridges that gap by creating a machine-readable vulnerability library and an intelligent scanner.

## Architecture: A Two-Phase Approach

The solution consists of two distinct phases:

### Phase 1: Building the Knowledge Base

Create a structured, local library of OWASP Top 10 vulnerability documentation optimized for LLM consumption.

### Phase 2: Intelligent Code Analysis

Use the knowledge base to perform context-aware vulnerability scanning on codebases.

## Phase 1: Automating Documentation Extraction

### The Meta-Prompting Strategy

Rather than hand-crafting prompts, this project uses LLMs to improve their own instructions. Starting with a rough prompt:

```markdown
Create a comprehensive prompt to accomplish the following:

1. Create a top level directory named "owasp-top-ten"
2. Scrape https://owasp.org/www-project-top-ten/
3. For each vulnerability, extract overview, descriptions, and prevention guidance
```

Claude enhanced this into a detailed, step-by-step workflow that handles edge cases, structures metadata consistently, and optimizes for downstream consumption.

### Automated Web Scraping Pipeline

The enhanced prompt drives Claude to:

1. **Extract the vulnerability index** from the main OWASP page
2. **Systematically scrape each vulnerability page** using WebFetch
3. **Structure data consistently** with metadata headers including:
   - Vulnerability name and OWASP category
   - Generation timestamp
   - Standardized sections (Overview, Description, Prevention)
4. **Generate clean filenames** using the pattern `A01-2021-Broken-Access-Control.md`

### Why Pre-fetch Instead of Real-time Scraping?

Pre-building the knowledge base offers several advantages:

- **Reduced context overhead**: Clean markdown vs. full HTML pages
- **Consistent formatting**: Standardized structure across all vulnerabilities
- **Offline capability**: No network dependencies during scanning
- **Version control**: Track changes to OWASP definitions over time

The library can be regenerated when OWASP updates their classifications, making it maintainable across different LLM providers.

Here is the current library in github at [owasp-top-ten](https://github.com/dmh2000/owasp-scanner/tree/main/owasp-top-ten).

## Phase 2: Context-Aware Vulnerability Scanning

### The Security Scanner Agent

Building on the knowledge base, the project includes a specialized security scanner that:

- **Systematically reviews code** against all OWASP Top 10 categories
- **Provides detailed analysis** with specific file locations and line numbers
- **Generates structured reports** for integration into CI/CD pipelines
- **Maintains focus on defensive security** practices

### Real-World Testing

The system was tested against deliberately vulnerable code examples:

**HTML/JavaScript Example**: A single-file web application with intentional vulnerabilities including:

- Cross-site scripting (XSS) vectors
- Injection vulnerabilities
- Insecure data handling
- Missing security headers

Here are the [results](https://github.com/dmh2000/owasp-scanner/tree/main/examples/simple-html/results.md)

**Python Example**: Server-side code with integrity failures:

- Insecure deserialization
- Dependency confusion risks
- Unsigned code execution
- Data integrity violations

Here are the [results](https://github.com/dmh2000/owasp-scanner/tree/main/examples/integrity-failure/results.md)

**A lot more validation would be required to turn this into a production ready tool.**

### Scanner Performance

The AI-powered scanner demonstrated superior contextual understanding compared to traditional static analysis tools:

- **Fewer false positives**: Understanding of application context
- **Comprehensive coverage**: Analysis across all OWASP categories simultaneously
- **Detailed explanations**: Not just "what" but "why" and "how to fix"
- **Language agnostic**: Effective across web, server, and application code

## Implementation Insights

### Prompt Engineering Best Practices

1. **Iterative refinement**: Start rough, let the LLM improve its own instructions
2. **Structured output**: Use metadata headers and consistent formatting
3. **Error handling**: Account for network issues and parsing edge cases
4. **Modularity**: Separate concerns (scraping vs. analysis vs. reporting)

### LLM Selection Considerations

The approach works across multiple LLM providers:

- **Claude**: Excellent at following complex instructions and web scraping
- **Gemini 2.5 Pro**: Strong analytical capabilities for code review
- **Adaptable**: Core approach transfers to other capable models

### Integration Opportunities

This foundation enables several advanced use cases:

- **CI/CD Integration**: Automated security gates in deployment pipelines
- **IDE Extensions**: Real-time vulnerability highlighting during development
- **Code Review Assistance**: Augment human reviewers with AI insights
- **Training Material**: Generate educational examples for security awareness

## Results and Impact

The system successfully identified multiple vulnerability classes that traditional scanners often miss:

- **Context-sensitive issues**: Understanding business logic flaws
- **Emerging patterns**: Recognizing novel attack vectors
- **Cross-file analysis**: Tracking data flow across application boundaries
- **Framework-aware scanning**: Understanding security implications of specific libraries

## Future Enhancements

Potential improvements include:

- **Custom rule development**: Extend beyond OWASP Top 10 to organization-specific risks
- **Integration with SAST tools**: Hybrid approach combining AI and traditional analysis
- **Continuous learning**: Update knowledge base with new vulnerability research
- **Team collaboration**: Shared knowledge bases across development teams

## Conclusion

This project demonstrates how LLMs can transform security tooling by combining web scraping automation, structured knowledge management, and intelligent code analysis. The key insight is treating LLMs not just as code generators, but as sophisticated reasoning engines capable of understanding security context and providing actionable guidance.

For development teams looking to integrate AI into their security workflows, this approach offers a practical starting point that can be extended and customized for specific organizational needs. The combination of automated knowledge base construction and intelligent analysis provides both immediate value and a foundation for more advanced security automation.

The complete implementation, including all generated documentation and example code, is available in the [project repository](https://github.com/dmh2000/owasp-scanner)
