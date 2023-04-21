---
tags:
  - MERMAID
---

# Trying to see if mermaid will work now

## Usage

### Using flowcharts

Flowcharts are diagrams that represent workflows or processes. The steps are rendered as nodes of various kinds and are connected by edges, describing the necessary order of steps:

Flow chart[^1]

``` mermaid
graph LR
  A[Start] --> B{Error?};
  B -->|Yes| C[Hmm...];
  C --> D[Debug];
  D --> B;
  B ---->|No| E[Yay!];
```

[^1]: Lorem ipsum dolor sit amet, consectetur adipiscing elit.
