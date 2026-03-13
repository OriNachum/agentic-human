---
layout: post
title: "Siri, do your magic"
date: 2024-01-23
tags: [automation, tutorial]
original_url: https://medium.com/@ori.nachum_22849/siri-do-your-magic-9a35f8098411
---

## Introduction

This is an article explaining how I integrated OpenAI's API with Apple products to empower Siri with generative AI, simplifying my daily life. This article covers the process, challenges, and solutions in detail.

### About myself

I'm the AI Experience Lead (AI Solutions Architects team lead) in Tipalti who enjoys automating processes in work and life.

## "Do your magic"

"Do your magic" is my iOS shortcut, callable by saying "Siri, do your magic" from my Apple Watch. It handles complex requests by splitting them into tasks and reminders.

I needed it to be able to perform complex actions on my phone when it's not reachable, from setting todo reminders, handling my shopping list to managing our baby's food and diapers log on WhatsApp.

I needed a solution — a framework — that I could expand to other actions as well, when the need arises.

### Why "Do your magic"?

It is the phrase I found most easy to say when I needed to perform actions on phone, but my hands are occupied.

Aspects I took into consideration:

1. Apple's speech to text had to understand my accent correctly in different devices (Apple Watch, iPhone, iPad).
2. A phrase that makes sense for the speech to text service (The speech-to-text services today have some self-correction mechanism).
3. A sentence that makes sense for me.

## Apple Ecosystem Tools

With Apple products, you can build no-code workflows using iOS Shortcuts. Shortcuts include coding features like loops, variables, and dictionary parsing along with system steps like HTTP requests. They can also access and perform actions from default apps like Reminders and Email, as well as many third party apps.

Recently, Apple improved Siri shortcut integration, allowing you to invoke shortcuts at the same time you wake Siri: "Siri, \<shortcut name\>" In comparison, before that, you had to say: "Hey Siri", then reply "\<shortcut name\>". This would have been cumbersome and annoying.

I leveraged these capabilities by using iOS Shortcuts to integrate OpenAI's API across my Apple Watch, iPhone, and iPad. I called this workflow "Do Your Magic." Now I can say "Siri, do your magic" on my watch to trigger it.

## Dive in: Building the Shortcut

### Constraints and Limitations

Not all steps are supported by all devices. It was crucial for me to set up a flow that allows me to call Siri's (And CGPT's) magic from watch.

This blocked a couple of basic options I really came to rely on:

- **Some apps are not supported:** Scriptable, DataJar and WhatsApp. Scriptable is an app that allows you to define scripts in basic JS, and have them run on iOS Shortcuts (or outside). DataJar is a neat app that allows setting up local storage that can be shared between flows. That way I can store data like "when I last ran the app?", and only refer to events that had occurred between now and last run, for instance. Note: there may be an unofficial WhatsApp solution — but I don't like sharing my information with 3rd party apps.
- **No files.** When working with GenAI, you might find yourself with overly increasing complexity prompts. It starts small, and grows — a lot — if you have big plans. As it happens, I do.

### iOS Shortcuts Steps

#### Ask OpenAI Chat

The first step I set up — even before this project — was a step for calling ChatGPT.

Now, you may tell me: Dude, you can do it via ChatGPT app, and spare the effort. You're absolutely right — that's what I initially did. Sadly, it's unreliable, and reliability is crucial here.

Then I turned to a step that implements OpenAI's API (I learned you can set up the payload on a text file — see the appendix in the end), it also used DataJar to share the key between steps (Which had served me well when I set up Image generation and Voice generation too).

This worked well for me, and still does, but failed for the watch — DataJar doesn't work on the watch. It was a small setback, and I created a new Watch-specific step where I keep the API key on the shortcut. (See Appendix about this)

### Main step: Do your magic

Once we get a request from the user (By narration, typing on keyboard, or share from some other location), the flow delegates some heavier tasks to sub steps.

#### Step 1: Split tasks

The first thing our shortcut needs to do is get an input — from that moment, it's impossible to programmatically parse it.

Sometimes I ask for changes like "five minutes ago" or "in five minutes". Sometimes it's a list of unrelated items, and we treat each item differently — let's see why.

Consider: "Log changing diaper with pee and poop to the baby, replace the changing diapers mat and buy new diapers and changing diapers mat"

We have 3 types of requests here:

1. **Log changing diaper with pee and poop to the baby:** This requires sending a WhatsApp message, which can't be done from the watch, but can be done by automation. I called it "Operable".
2. **Replace changing diapers mat:** This is a "Todo" list item. I cannot order it automatically (no such Amazon services here).
3. **Buy new diapers and changing diapers mat:** This is a "Shopping list" item and I want to split it by items.

The order and words I use to request each of these is often changing (By mistake or just mood). I needed flexibility.

**Solution:** Use Call ChatGPT with an appropriate prompt, so it splits my request and sorts it into the appropriate "Dictionary of dictionaries" json format. It's highly reliable!

Once I did that, I only had to clean up the markdown code wrapping for json, and parse it with an appropriate step.

#### Step 2: Parse Intelligent Reminders

The above "Do your magic" step starts to get complex, and we have further work to do. It is a good time to split our work to a new task.

In "Do your magic" we iterate over the first level of keys in the dictionary — they represent the list names. Now we look at each subset of items in list and place it in the correct list accordingly. This means placing all items in the appropriate list by the key given, and a specific format.

Is that all?

What we have now is smart reminders, but not smart enough. Nothing handles anything once a reminder was created. Let's cover the automated part.

### General — automation

In iOS Shortcuts you can also set up automated steps. These run on specific trigger, and not shared between devices.

I initially set about 10 reminders, each spaced by approximately 2 hours, to test the basic functionality.

Following this, I streamlined the process by creating a trigger based on a specific self-sent email, which efficiently activates the 'Do your magic' shortcut.

So, what do these triggers do? Handle operables!

#### Step 3: Handle operables

Operables are items I know how to automate an action when they are processed.

We read them one by one, while unread in 'Operables' list, treat them separately, and mark them as 'read'. This step is also split into a subtask, for simplicity.

So it handles working with the list, but 'treat them' as mentioned above, is a new step: "Handle operable reminder"

#### Step 4: Handle Operable Reminder

This step has instructions what to do, and does it.

At its current stage, it just sends a message to a channel or private conversation on WhatsApp according to the requested format.

At later stage, I will have steps per action and the step will trigger the correct shortcut per the instructions it gets from a GPT call.

## Summary

With this set up I can ask a complex request, that is processed by OpenAI API, splits the tasks into relevant targets and triggers the 'automated handler'.

The automated handler reads the list and sends WhatsApp messages as needed.

## Your thoughts?

I'd love to hear your feedback, questions and suggestions about this, I love feedback!

Have you integrated generative AI API, OpenAI or otherwise, in your life? (Not a 3rd party service, but actual API where you define the prompt and actions, not GPTs either)

Interested in this solution? Let me know — I'll be happy to share this with you and spare the effort of building any of the steps.

Please let me know in the comments, and thank you for reading!

## Appendix

### Use text for complex payload: HTTP request

You will notice the "Get contents of" step, can actually do all Methods, and specifically POST. However, some requests are just too complex, and you need a dictionary with dictionary with dictionary to make the API run.

Instead of setting it up manually (don't do it to yourselves!), set it on a text step, and send that instead. You can choose a text variable, if you had set up the request body to be "file".

### Shared storage: Reminders and Mail

As mentioned, Apple Watch is currently limited, and can't use notes and files. You can always use a dedicated list in Reminders, or send yourself an email to get some form of shared storage.

### Shortcut configurations

#### Context

If you go to your shortcut and press the same (i) button below, you get a screen of configurations. This includes where this shortcut appears. I like:

- **Apple Watch:** So I can also select this manually on the watch (But filter out those I don't use)
- **Quick Actions:** So I can mark the tasks my wife and I wrote to ourselves, press "share" and send it directly to this "Do your magic" shortcut. Nifty.

#### Setup

Another useful configuration there is setting under 'Setup' tab. It allows you to select which values in the shortcut needs to be provided by the user. This allows you to use a secret in the step, but when exported/imported, the system will ask the user to provide a value relevant to them.

### Special thanks

Special to Zachary Leighton, Allen Jacobson and Viki Bar for reviewing this before publish.
