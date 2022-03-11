---
layout: post
title: In Support of the “Snacklog”
categories: twiki
---

Recently we’ve noticed a number of our clients maintain a backlog of small tasks that are handled separately from their main backlog. These are tasks that should be finished at some point, but will rarely take priority over business-critical features and bugfixes. Often they are bite-sized pieces of work that can be finished in a couple of hours or less: addressing engineering chores, paying off tech debt, and addressing minor bugs. Internally, this separate backlog has earned a catchy name: **the snacklog**.

When is it appropriate to work on a snacklog task instead of something in the prioritized backlog? After all, developers should be working on things that move the business forward (obviously). Inevitably, though, natural lulls come up in the course of development:

1. I’ve just finished a big pull request and have some time before my team finishes leaving feedback.
2. I’m temporarily blocked by a design or product decision.
3. It’s near the end of the day, and I’d rather work on something small than start a big feature.
4. I’m totally new to the team and need to get acquainted with the code base.

In any of these cases, it’s valuable to maintain productivity by picking from a set of curated 5-minute to 2-hour tasks–tasks that would be estimated below 2 points.

## So what belongs in the snacklog?

* Copy changes that aren’t urgent
* Small UI bugs, for example, affecting only one browser
* Bugs in an admin UI
* Updating documentation
* Small, meaningful refactors. For example, extracting common CSS variables and mixins.
* Removing dead code paths, which itself can be considered a form of documentation by removing patterns you don’t want to be imitated.
* Phasing out feature flags or successful experiments that are 100% rolled out
* Review lingering TODO comments
* Fixing an intermittently failing test or speeding up a slow spec
* Updating dependencies to their latest patch level. Let’s hope your dependencies are semantically versioned properly!
* Extracting reusable React or Angular components

## What does not belong in the snacklog?

* Time-sensitive feature development
* **Critical** copy changes and bugfixes. These should be prioritized through the normal channels.
* Updating vulnerable dependencies. This should also be prioritized through normal channels. I don’t have any expectations that snacklog tasks will be finished in a given time frame, and I would rather not allow vulnerable dependencies to go forgotten for a long stretch of time.
* **All** larger technical debt tasks. Large chunks of tech debt cannot be paid back intermittently, two hours at a time. Make sure you can prioritize larger tech debt chores as part of a normal sprint/iteration.
* Anything else that would take longer than a couple of hours of work.

There are extra benefits to maintaining a snacklog:

1. New members to a team can ease into an unfamiliar code base.
2. Junior members can take on more autonomy in fixing a bug or working on a chore.
3. Everyone can maintain their momentum in a sprint, even when they are blocked or waiting for code review.
4. Tech debt is more visible to the team and can be tackled incrementally.

Before you rush into setting up a snacklog for your own team, bear in mind this process may not fit every team. It requires a level of trust with the product owner and developers who are careful to pull from the snacklog sparingly. It’s tempting to procrastinate on high priority work by clearing out easy tasks first. The team should agree not to let snacklog progress get in the way of working on stories in the active sprint/iteration. Developers on the team should be disciplined enough to recognize if a snacklog task will end up taking longer than a couple of hours. Large tasks can either be split into smaller tasks or be added back to the original backlog for proper prioritization.

I’ve personally found it satisfying to have small snacklog wins peppered throughout the week. Here’s hoping you’ll get the same enjoyment too.
