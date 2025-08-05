---
author: David Howard
pubDate: 2025-01-28
title: Adding AI To Golang Apps
postSlug: golang-ai
featured: true
draft: false
description: 'Three approaches to using AI models in Golang'
---

# Throw Some AI Into Your Go Application

It seems to be popular, if not mandatory, to add AI to apps, whether they need it or not. It turns out that with Go its reasonably easy to make queries to AI from inside a Go program. Assume you want to connect to an AI LLM provider, send it a query and get the results back.

When integrating Large Language Models (LLMs) into your Go applications, there are several approaches you can take. This post explores three different methods using the Sqirvy client library as examples.

- HTTP API
- Native Library
- LangChain

## The Code

The full code described here is in [github.com/dmh2000/sqirvy-llm](https://github.com/dmh2000/sqirvy-llm), along with example usage in command line programs and a sample web app. The code includes support for Anthropic, Meta-llama, OpenAI and Gemini models.

This Go library implements methods for simple queries to various AI providers.

The directory structure for sqirvy-llm. (abbreviated)

<pre>
├── pkg
│   ├── sqirvy             (what this post is about)
│   │   ├── anthropic.go   (use the anthropic native library)
│   │   ├── client.go      (the interface)
│   │   ├── meta-llama.go  (use LangChain)
│   │   ├── openai.go      (use HTTP API)
│   └── util
├── cmd (example programs)
│   ├── sqirvy-query  (make a simple arbitrary query)
│   ├── sqirvy-review (specialized to request a code review)
│   └── sqirvy-scrape (scrape a website and get a markdown layout)
└── web
    └── sqirvy-web (a simple web app to compare LLMs)

</pre>

## How It works

### Creating a Sqirvy Client

The Sqirvy library provides a unified interface for interacting with various LLM providers using the different approaches to coding a simple text query.

To create a client:3

```go
import "github.com/dmh2000/sqirvy-llm/pkg/sqirvy"

// Create a client for your chosen provider
client, err := sqirvy.NewClient(sqirvy.OpenAI) // or Anthropic, MetaLlama, etc.
if err != nil {
    log.Fatal(err)
}

// Make a simple query
response, err := client.QueryText("Tell me a joke", "gpt-4-turbo-preview", sqirvy.Options{})
```

### Three Integration Approaches

#### 1. Direct HTTP API Integration (OpenAI Example)

The most straightforward approach is to directly use the provider's HTTP API. This gives you complete control but requires more boilerplate code. Here's how OpenAI integration works in Sqirvy:

OpenAI HTTP API: https://platform.openai.com/docs/api-reference/introduction.

sqirvy-llm: https://github.com/dmh2000/sqirvy-llm/blob/main/pkg/sqirvy/openai.go

```go
// OpenAI client using standard HTTP requests
type OpenAIClient struct {
    apiKey string
    client *http.Client
}

// Make a request
jsonBody := openAIRequest{
    Model: model,
    Messages: []openAIMessage{
        {Role: "user", Content: prompt},
    },
}
// Send HTTP POST request to OpenAI endpoint
```

Advantages:

- No external dependencies
- Full control over request/response handling
- Easy to debug and modify
- Direct mapping to API documentation

Disadvantages:

- More boilerplate code
- Need to handle HTTP details manually
- Must implement retry logic yourself

#### 2. Official SDK Integration (Anthropic Example)

Using an official SDK provides a more polished experience with built-in types and error handling.

Anthropic Go SDK: https://github.com/anthropics/anthropic-sdk-go

sqirvy-llm: https://github.com/dmh2000/sqirvy-llm/blob/main/pkg/sqirvy/anthropic.go

```go
// Anthropic client using official SDK
client := anthropic.NewClient()

message, err := client.Messages.New(context.TODO(), anthropic.MessageNewParams{
    Model: anthropic.F(model),
    Messages: anthropic.F([]anthropic.MessageParam{
        anthropic.NewUserMessage(anthropic.NewTextBlock(prompt)),
    }),
})
```

Advantages:

- Type safety
- Built-in error handling
- Official support
- Automatic retries and best practices

Disadvantages:

- Dependency on external package
- Less flexibility for customization
- May lag behind API updates

#### 3. LangChain Integration (Meta Llama Example)

Using LangChain provides a unified interface across multiple providers. LangChain has official SDK's for
Python and Javascript but not Go. There is an 'unofficial', but popular and well tested Go SDK.

LangChainGo: https://github.com/tmc/langchaingo

https://github.com/dmh2000/sqirvy-llm/blob/main/pkg/sqirvy/meta-llama.go

```go
// Meta Llama client using LangChain
llm, err := openai.New(
    openai.WithBaseURL(baseURL),
    openai.WithToken(apiKey),
    openai.WithModel(model),
)

completion, err := llms.GenerateFromSinglePrompt(context.Background(), llm, prompt)
```

Advantages:

- Unified interface across providers
- Rich ecosystem of tools and chains
- Easy to switch between providers
- Community support

Disadvantages:

- Additional abstraction layer
- May not expose provider-specific features
- Larger dependency footprint

## Choosing an Approach

Consider these factors when choosing an approach:

1. **Direct HTTP API** if you:
   - Need complete control
   - Want minimal dependencies
   - Are only using one provider
   - Need to match API docs exactly

2. **Official SDK** if you:
   - Want type safety and official support
   - Need built-in best practices
   - Are primarily using one provider
   - Value ease of use over flexibility

3. **LangChain** if you:
   - Need to support multiple providers
   - Want access to higher-level abstractions
   - Plan to build complex chains
   - Value provider interchangeability

## Conclusion

Each approach has its merits, and the choice depends on your specific needs. Sqirvy demonstrates all three approaches, allowing you to see how they work in practice and choose the one that best fits your use case.

Remember to always handle your API keys securely and respect rate limits regardless of which approach you choose.
