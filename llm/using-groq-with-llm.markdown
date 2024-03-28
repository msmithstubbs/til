# Configure llm to query groq from the command line.

[Groq](https://groq.com) is a startup developing their own inference hardware. They have an impressive demo that returns results from publicly available large language models with sub-second response times.

Groq also has an API that mimics the OpenAI chat completion API. It turns out to be quite simple to configure [llm](https://llm.datasette.io/) to call groq's API instead of OpenAI.

First, get a an API key for groq from [https://console.groq.com/playground](https://console.groq.com/playground)
You can save the key in llm:

```bash
llm keys set groq
```

Then, configure llm to use the groq API. Add this to `extra-openai-models.yaml`

```yaml
- model_id: groq
  model_name: mixtral-8x7b-32768
  api_base: "https://api.groq.com/openai/v1"
  api_key_name: groq
```

This file is stored in the llm config directory. On a Mac it should be `~/Library/Application Support/io.datasette.llm`

That's it. You can now select groq when you run llm:

```bash
llm -m groq "Tell me a joke about giraffes"
```
