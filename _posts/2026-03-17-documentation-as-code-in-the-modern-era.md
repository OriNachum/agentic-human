---
layout: post
title: "Documentation as Code in the Modern Era"
date: 2026-03-17
tags: [documentation, agentic-ai, developer-experience, notebooklm]
toc: true
original_url: https://medium.com/@ori.nachum_22849/documentation-as-code-in-the-modern-era-c53e3a34c722
---

The concept of Documentation as Code is solid. GitHub supports it with GitHub Pages or with pipelines (Markdown to Confluence) for a long while now. Let's build on this solid foundation.

## Documentation as Code

Documentation as Code is a well-established practice. We even see new and renewed concepts like Code as Documentation (Agent Skills) I mentioned in my [previous article](/2026/02/24/code-as-documentation-the-role-of-agent-skills/).

## The Compiler

Today, I want to take this further.

There are several tools relevant for Docs as Code: IDEs, SSGs (Doc to Site), CI/CD, Linters/Validators.

To add to this list, I propose we add the compiler.

The compiler in this case will be a tool we use to merge multiple files into a new modality: The new modality can be reflected as user stories, Audio/Video Overview, Infographic, a discussion between different entities, and more.

Then, consume that new modality and reflect upon it — this step is critical, as it puts you back in the core of the process.

## Documentation as Tests

This process digests and merges the content to a story you can guide, make decisions, and repeat gradually.

As you do, you may find inconsistencies, perhaps your agentic coder (or human coder) misunderstood you or took some liberties at implementation.

Sometimes it's good and you learn something new, and sometimes it is bad or even catastrophic.

That kind of evaluation is at a higher level: an Overview.

## Compiler Options

My favorite "compiler" for this is NotebookLM. I use it often to digest my docs into images, audio, and video, and then consume them. It offers different modalities and setups, and you can select different sources on each generation.

Another option is working with your favorite agent to generate any modality you like — paper articles, a game, a story.

## Risks

Working like that isn't 100% — but neither is any type of test.

It gives you a high concept overview, makes sure the features align, but it has some caveats:

- Different AI models tend to process content differently.
- - AI sycophancy could stray you away from improvement.
  - - It may foster a sense of false confidence.
   
    - Adopt a suspicious mindset and use it to get an understanding of what was created, but it cannot be your only way to assess your code.
   
    - **Tip:** Asking the AI to be brutally honest, or asking for a Critique persona can help.
   
    - It doesn't replace code tests, and exploratory testing to see how your product feels.
   
    - ## Human in the Core
   
    - I highly value human decision making, and AI can work perfectly on top of that. When creating documentation — go lazy about the writing, but be critical and deliberate about "the what?".
   
    - Use clean context, ask the agent to write docs for specific components you deem important.
   
    - Explore your code as you ask the Agent about architecture, components, features — you may want to ask about "agents" in your code, but dive deep for a specific agent with higher complexity.
   
    - Think of how you want to describe this to someone else, what is important and what is irrelevant.
   
    - It's ok to make mistakes — you may find it's not relevant when you consume it later, and you can always make changes or generate your docs anew.
   
    - Don't be afraid of refactoring your docs — it's a needed process, like refactoring code or tests.
   
    - ## Treat Your Documentation as Production Code
   
    - With this setup, documentation is no longer a byproduct you have to generate because your boss told you, company policy or because "it is right" — now this is an essential part of your creation, just like tests are crucial for your success.
   
    - It essentially eliminates the docs going stale and puts them as part of your pipeline.
   
    - ## Live Demo
   
    - When I fed this original document, I did 2 things:
   
    - 1. I opened Claude Plugin on Chrome, and asked it for feedback.
      2. 2. I copied it to NotebookLM, and requested 3 modalities I like: Infographic, Video Overview, Audio Overview.
        
         3. As NotebookLM was generating the content, I talked with Claude about what's missing — the process itself drives my thinking toward criticism.
        
         4. From these 2 processes, I realized the article was missing 3 items:
        
         5. 1. Visualizing the process with a Live Demo — this is this section!
            2. 2. Risks: Hallucinations, Agent Biases, False confidence, complementary process.
               3. 3. Human in the Core: detailing the documentation creation flow.
                 
                  4. I corrected them, and promptly added this section — but it took another 2 iterations (total of 4 versions) to get to this article.
                 
                  5. ## Now It Is Your Turn
                 
                  6. What modalities would you favor? How does that meet your own projects?
                 
                  7. I would love to hear your thoughts in the comments, and hear what you think about this concept of Compiler for Documentation as Code.
