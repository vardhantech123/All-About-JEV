## What is JEV?

JEV is TypeSafe AI’s first **System One model**, launched in early access on **September 15, 2026**. Unlike traditional LLMs that generate free-form text, JEV takes **unstructured state + typed questions** and returns **typed, probabilistic decisions** (e.g., Choice, Score, yes/no) that software can consume directly. [marktechpost](https://www.marktechpost.com/2026/09/19/typesafe-ai-releases-jev/)

It is designed for **fast, structured decision-making** in agents, routers, guardrails, trading systems, and other automation pipelines, with reported latency of **70–500 ms** and costs around **$0.042 per 1M input tokens**, with **free output tokens**. [marktechpost](https://www.marktechpost.com/2026/09/19/typesafe-ai-releases-jev/)

***

## Key Characteristics

- **Not an LLM**: Transformer-based but does **not generate text**. [marktechpost](https://www.marktechpost.com/2026/09/19/typesafe-ai-releases-jev/)
- **Output types**:  
  - `Choice` – select from predefined options  
  - `Score` – numeric score with confidence  
  - `Noul` – yes/no/uncertain with probability [github](https://github.com/kraayenjon/awesome-jev)
- **Speed & cost**: Claimed **20–200× faster** and **40–400× cheaper** than frontier LLMs for decision tasks. [datacamp](https://www.datacamp.com/blog/system-one-models-jev)
- **Access**: Hosted API only (closed weights). Available via:
  - TypeSafe waitlist: `https://api.typesafe.ai/v1/systemone`
  - Vercel AI Gateway: model ID `typesafe-ai/jev`
  - Cloudflare Workers AI: `typesafe/jev` [github](https://github.com/kraayenjon/awesome-jev)

***

## Example API Usage

```http
POST https://api.typesafe.ai/v1/systemone
Content-Type: application/json

{
  "state": "User message: 'I want to cancel my subscription.'",
  "model": "jev-latest",
  "questions": {
    "intent": {
      "type": "Choice",
      "options": ["cancel", "upgrade", "billing_question", "other"]
    },
    "urgency": {
      "type": "Score",
      "min": 0,
      "max": 10
    },
    "is_complaint": {
      "type": "Noul"
    }
  }
}
```

Response (simplified):

```json
{
  "intent": {
    "decision": "cancel",
    "probabilities": {
      "cancel": 0.92,
      "upgrade": 0.03,
      "billing_question": 0.03,
      "other": 0.02
    }
  },
  "urgency": {
    "decision": 7.4,
    "confidence": 0.88
  },
  "is_complaint": {
    "decision": "yes",
    "probability": 0.81
  }
}
```



***

## Suggested GitHub Repo Structure

You can create a repo like `awesome-jev` or `jev-examples` with:

- `README.md` – overview, quickstart, links
- `examples/` – sample integrations (Node, Python, etc.)
- `integrations/` – LangChain, Vercel, Cloudflare snippets
- `projects/` – curated list of real-world JEV projects
- `resources/` – links to docs, announcements, talks

Several community “awesome-jev” lists already exist and can be used as inspiration or linked as related projects. [github](https://github.com/kraayenjon/awesome-jev)

***

## README Template (Copy-Paste Ready)

```markdown
# JEV – TypeSafe AI System One Model

**JEV** is TypeSafe AI’s first **System One model**: an AI “decision engine” that returns **typed, calibrated probabilities** instead of text. It is optimized for software-driven decisions such as routing, classification, scoring, guardrails, and agent control.  [marktechpost](https://www.marktechpost.com/2026/09/19/typesafe-ai-releases-jev/)

## Highlights

- **No text generation** – outputs structured decisions (`Choice`, `Score`, `Noul`) with probabilities.  [github](https://github.com/kraayenjon/awesome-jev)
- **Very fast & cheap** – designed to be 20–200× faster and 40–400× cheaper than frontier LLMs for decision tasks.  [latent](https://www.latent.space/p/ainews-jev-a-system-one-model-that)
- **Hosted API only** – model weights are not public; access via TypeSafe, Vercel AI Gateway, or Cloudflare Workers AI.  [github](https://github.com/yibie/awesome-jev)

## Access

- Join the early-access waitlist: https://typesafe.ai  
- Vercel AI Gateway: model ID `typesafe-ai/jev`  
- Cloudflare Workers AI: `typesafe/jev`  

API endpoint (early access):

```http
POST [https://api.typesafe.ai/v1/systemone](https://api.typesafe.ai/v1/systemone)
```

 [github](https://github.com/yibie/awesome-jev)

## Example Use Cases

- Intent classification & routing for chatbots
- Real-time trading signals (buy/sell/hold)
- Content moderation & policy guardrails
- Agent action selection (which tool to call next)
- Scoring leads, tickets, or user messages by urgency/quality  [github](https://github.com/kraayenjon/awesome-jev)

## Resources

- Launch announcement & docs: https://typesafe.ai  
- “101 Real-World Examples of How to Use Jev”: https://hackernoon.com/101-real-world-examples-of-how-to-use-jev  
- Community lists:  
  - https://github.com/yibie/awesome-jev  
  - https://github.com/kraayenjon/awesome-jev  
  - https://github.com/cobanov/awesome-jev  [github](https://github.com/kraayenjon/awesome-jev)

## License

Add your preferred license (e.g., MIT) if you’re publishing examples or tooling. The JEV model itself remains proprietary and hosted by TypeSafe AI.  [gist.github](https://gist.github.com/drillan/6916b16e8ea31a8ec36c8f59d6483150)
```
