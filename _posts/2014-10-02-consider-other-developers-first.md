---
layout: post
title: Consider Other Developers First
permalink: /blog/consider-other-developers-first/
---

[Maintaining a clean codebase](http://ericnish.io/blog/the-importance-of-clean-code) is a good start for keeping your buddies happy, but it helps little if building and deploying the code demands esoteric knowledge. And remember, you (or rather—the future you) are also your own naïve team member, so working in solitude doesn't guarantee that you'll remember everything six months from now.

What I want to stress is that, in order to maintain efficiency and a comfortable programming experience, you should serve everything you create on a silver platter. Make everything as easy to pick up, understand and extend as you can. Be a mindful developer experience designer.

Few of us like to skim through a lengthy readme file (or fragments of documentation from multiple sources) that was updated over the course of 30 commits just so we can get the latest changes to work after a merged feature branch. Stick to simple conventions. Plan ahead. Imagine yourself in the shoes of the least experienced developer on the team. Try to make things easy for your buddies. Please. Preeease.

If convention holds that running 'update.sh' after a 'git pull' makes everything work, make sure you don't violate the rule. The least you can do is test it in your local environment. Try not to further complicate things by polluting the readme file with new deployment steps and instructions for the feature you just merged into a stable branch. Keep the readme concise and digestible by making your changes seamless and unnoticeable to the developer.

Your fellow developers already have their JIRA accounts brimming with tasks pending to be solved, so overburdening them with suboptimal solutions (out of laziness) is rather inconsiderate. A new feature that consumes an undesirable amount of time and effort to deploy is already a bug in itself. If you need advice, consult a senior (or the web) and figure out a sound solution instead of resorting to a poor alternative and eventually blocking the entire team.

Also bear in mind that cultures vary. And another project's planning, coding and deployment routines may sound alien to you. Unfortunately you may not always have the authority to amend formerly established conventions. But what you can do is strive to provide the most comfortable programming experience for other developers within the boundaries of the project's current state of affairs.

If you are certain that a project's workflow is on the brink of collapse, you have all the right to bring it to the team's attention. Carefully crafted code requires a greater time investment, but a heap of hurried hacks entails an infinite amount of wasted development time without brave intervention.

While a beautiful end product may satisfy the client, a polished codebase keeps the developers sane; and it's the team's job to make everyone happy.
