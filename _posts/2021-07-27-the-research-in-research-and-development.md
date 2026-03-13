---
layout: post
title: "The \"Research\" in \"Research & Development\""
date: 2021-07-27
tags: [culture, developer-experience]
original_url: https://medium.com/@ori.nachum_22849/the-research-in-research-development-b9d8d25f897
---

I'd like to share my experience of exploring technologies, and refer to a different meaning than the usual meaning given to "Research" in "Research & Development".

Our SVP of R&D had provided us a way to value ourselves as developers:

On the bottom line, a developer is measured by their impact. The impact is reflected by actions, and you can act only out of knowledge.

**Knowledge → Action → Impact.**

Therefore, to make an impact, to be able to do something that affects the company, or the community — we need to obtain more knowledge.

During development, we're often asked to do something; work with a new API, or use a certain tool or framework.

I've come to find, many developers do "The minimum requirement". We find "a way that works" and then fall to the good old habit of "if it works, don't touch it".

When we break that habit but do it smartly, we can improve our effectiveness, and eventually increase everyone's productivity.

Below are a few examples of how exploring further from my scoped tasks, had led to global improvements in the company, that benefited all of us.

## Slack Integrations

On our latest company Hackathon, almost everyone put their hands on machine learning. While we learned a lot about what we were lacking to incorporate more in our product, I got another lesson: Slack integrations are easy!

Our tool was a closed system that detects incoming food deliveries that notifies what food had arrived. Aside from learning how to use a model and train it with new data, we needed to output the result to our company chat app.

With Slack integrations, it was very easy, as they provide custom WebHooks.

This had later led me to play with Kibana's alerting system, which now we use for active monitoring (In addition to Grafana), and get to issues instead of wait for someone to notice them — reducing customer friction.

I was doubly benefited, when I had also used that for my private Slack, and set up my baby's food & diaper change updates from the phone, for my wife and me.

A dedicated channel and an HTTP Client app that supports variables made keeping track of that history a 3-button clicks effort.

## Loki — A Chrome Extension

Our Frontend Architect (Zachary Leighton) had set up a frontend testing framework called Percy (Serverless UI). It uses Puppeteer to interact and requires us to mock any HTTP call required to reach our desired screen. Then you can take a screenshot, and it compares by pixel to the latest approved change.

It meant a lot of searching and copy-pasting from Developer Tools different tabs (Network & Elements). Also, we had to filter out irrelevant information and click each relevant call.

During the Coronavirus epidemic, Udemy had released free courses, and I grabbed what was available. One of these was writing chrome extensions (2hr course that could have been shorter).

It pushed me to develop something — it's easier to learn a new technology when you try to do something you need or fix something that bothers you.

I practiced this knowledge to write a small monitoring chrome extension (Loki) that collects all relevant information (Only on our test sites, so we don't peek into everyone's browsers), puts it in a single place in the format of our Percy tests.

It made writing those tests much simpler.

As a bonus, another dev had used the code to learn & write his own tool (Kept in our shared tooling repository), a different QOL extension that now makes our lives better.

## F# & Azure DevOps integrations

Our company uses Azure DevOps to manage our Git repositories.

As a team leader, I wanted Slack updates (Remember? Slack Integrations are easy!) and set up a tool that reads our Pull Requests, connects them to Jira, and sends an update to Slack.

Our Backend Architect (Rotem Kirshenbaum) exploration of F# and .NET features had guided me to properly write a parser that sends the AzureDevops API responses to Slack. It worked great but wasn't as useful as I envisioned it, and it required more work — but I kept the code in our tooling repository, and found different ways to use it!

This had resulted in 3 different tools:

### MSTest to XUnit converter (F#)

This allowed moving our tests from the MSTest framework, used by our legacy code, to the recommended XUnit framework.

### Detailed Test notifications (AzureDevops API)

This had spared us the need to go to another system (Out of Slack, to AzureDevops), provided us better visibility of failing tests, and allowed searching test history in a dedicated Slack channel.

### Alfred: An Auto-merge tool between our legacy branches: master → release → dev (Git, Slack & AzureDevops .yml pipeline)

This had alleviated the great pain of keeping the commits aligned and reduced the risk of conflicts.

Each one made our lives simpler in different ways, and each is an example for other developers to write their own solutions.

## Sharing is caring

A key to impact is sharing.

When we write a tool and share it with others — we impact our friends. When we get feedback for it — we also impact ourselves. Our tools improve, our skills improve.

When we share our code — we encourage others to improve it themselves or write their own solutions. This later impacts everyone on a bigger scale.

When we share ideas — the scale grows larger.

As our company grew, we found more and more makers; developers write tools that make everyone's life easier, not just because "It's their job".

I found developers contact me to get advice on how to approach new tools (As I once did when I wrote "Loki"), and felt we needed a place.

It led me to open a single place for sharing ideas, getting feedback, and overall a place that encourages you to create. In Slack, I gave the channel the informal name: Shai-Hulud (Named after Dune's giant worms, also called "Makers"), In Confluence, I added a formal place: Tipalti Innovation Center.

This had improved communication, sharing & brainstorming, and encouraged developers to be part of this new place.

I believe it is a start of a "Guild" for makers (The concept of guilds was introduced to me by my team leader— now my director, Rotem Benjamin), and in itself, an impact on the company.

## In Conclusion

Part of a developer's value is in research, and developers who can research out of their defined scope, are "wildcards" in the company.

If they focus right (Not forgetting their actual work), they can benefit the company greatly.

The "Makers" value grows exponentially as they share knowledge, ideas and eventually become a community — a makers guild.
