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

``` mermaid
graph TD
A[/home/raneydazed/pr/] -->|contains| B[.git/]
A[/home/raneydazed/pr/] -->|contains| C[.gitmodules]
A[/home/raneydazed/pr/] -->|contains| D[...]
A[/home/raneydazed/pr/] -->|contains| E[sub-mod/]
E[sub-mod/] -->|contains| F[.git/]
E[sub-mod/] -->|contains| G[...]
```

[^1]: This is a footnote. Pretty fuckin rad amirite
