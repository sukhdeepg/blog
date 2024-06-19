---
title: "Engineering blogs list"
date: 2024-05-26T15:10:01+03:19
draft: false
showToc: false
TocOpen: false
cover:
    image: img/engineering-blogs.png
    alt: "engineering_blogs"
tags: ["engineering-blogs"]
---

* [Musings on building a Generative AI product](https://www.linkedin.com/blog/engineering/generative-ai/musings-on-building-a-generative-ai-product)
    The team aimed to improve job search and content on user's feed by using generative AI. Allow faster access to information, connecting relevant content, offering advice, and more personalized experiences.
    1. **Development Process**:
       - **Overall Design**: Implementation of Retrieval Augmented Generation (RAG) pipeline for efficient handling of user queries. Routing (Valid query check and selecting AI agent), retrieval (selecting which services to use), generation (generating the final response).
       - **Development Speed**: Split tasks into independent agents for faster development across teams.
       - **Evaluation**: Faced challenges in evaluating answer quality, tackled through guidelines, scaling annotation, and automatic evaluation.
       - **Calling Internal APIs**: Internal APIs are called, and their responses are injected into a subsequent LLM prompt to provide additional context to ground the response.
       - **Consistent Quality**: The team initially achieved 80% of their targeted experience within a month using generative AI, but faced challenges in detecting and mitigating errors, leading to a slower rate of improvement and a shift towards more prompt engineering to fine-tune large language models for a more data-driven pipeline.
       - **Capacity & Latency**: Balanced quality, throughput, and member latency while managing GPU cluster costs and optimizing response times.
    2. **Ongoing Work**:
       - Refining LLM training for a more data-driven approach.
       - Enhancing deployment infrastructure for better predictability and efficiency.
       - Reducing latency and wasted tokens in the pipeline.
* [Building Meta’s GenAI Infrastructure](https://engineering.fb.com/2024/03/12/data-center-engineering/building-metas-genai-infrastructure/)
* [Shepherd: How Stripe adapted Chronon to scale ML feature development](https://stripe.com/blog/shepherd-how-stripe-adapted-chronon-to-scale-ml-feature-development)
* [How Stripe’s document databases supported 99.999% uptime with zero-downtime data migrations](https://stripe.com/blog/how-stripes-document-databases-supported-99.999-uptime-with-zero-downtime-data-migrations)
* [How data is powering skills-based hiring on LinkedIn](https://www.linkedin.com/blog/engineering/talent/how-data-is-powering-skills-based-hiring-on-linkedin)
* [Developing Rapidly With Generative AI](https://discord.com/blog/developing-rapidly-with-generative-ai)
