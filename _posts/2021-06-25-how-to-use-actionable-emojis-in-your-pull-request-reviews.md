---
layout: post
title: How to Use Actionable Emojis in Your Pull Request Reviews
categories: twiki
---

Carbon Five has embraced emoji in daily written communication. They carry a lot of meaning in a small package, they inject personality and culture into our writing, and they visually stand out on the page as you scan a document. Pull requests are no exception. Love them or hate them, emojis ensure our pull request comments include the intended tone, something easily lost in written communication.

An engineer has only two strong signals to summarize their whole response to a PR: approve or reject. But what about all of the smaller, intermediate comments? Consider prefacing a review comment with different emoji to classify the comment under one of these three categories. (Many thanks to Srinivas Rao for his [initial write-up](https://gist.github.com/raorao/a8f01657ef600157958180832bdc28fe) that inspired this strategy.)

1. **Positive, congratulatory** comments that give kudos and compliment the author for his or her work. The pull request author is not required to respond to these.

To stick to *green* emojis:

* 💚 green heart
* ✅ check mark button

See also:

* 😍 smiling face with heart-eyes
* 🏆 trophy
* 💯 hundred points
* 🌈 rainbow
* 🦄 unicorn

Examples:

```
💚 Thanks for adding test coverage!
```
```
🏆 omg finally
```
```
🦄 No code is the best code
```

2. **Non-blocking questions** that ask for clarification, or for non-blocking suggestions for a **refactor** or other **cleanup**. The pull request author is free to merge his or her work, but should consider answering any questions and addressing concerns. It’s the polite thing to do!

To stick to *yellow* emojis:

* 🤔 thinking face
* 💡 light bulb
* ⚠️ warning
* ⚡️ lightning bolt
* 🔔 bell
* 🎨 artist palette (read as “code style”)

See also:

* ❔ white question mark
* 💭 thought balloon
* 💬 speech balloon

Examples:

```
🤔 Out of curiosity, when would I choose to use this over StillSupportedClass?
```
```
⚠️ Heads up, this may end up conflicting with a change in #4321. Please coordinate with them to ease the merge.
```
```
🎨 In the past I have used the classnames package to handle conditional styles. Do you have a preference?
```

3. **Blocking** comments that **must** be addressed before the pull request can be merged. Pair these with a “Request Changes” review to emphasize that follow-up is required.

To stick to *red* emojis:

* ❗️exclamation mark
* 🚨police car light
* 🛑 stop sign
* ❌ cross mark
* 🪓 axe
* 🧨 firecracker

Examples:

```
🛑 Renaming a database column ties up this particular database for too long. Please add a new column first and copy the data before dropping the old column.
```
```
🚨 This change would reintroduce a bug we fixed a few months ago. See #4455 for more context.
```
```
🪓 These updates don’t seem to be related to the current PR and would best be introduced in a separate PR.
```

# Frequently Asked Questions (As The Author)

## Someone left a blocking comment on my pull request that I do not believe is blocking. What should I do?

Your first instinct should be to trust your team. If your teammate believes an issue is blocking, they are likely making that determination intentionally, based on their unique experience. Respect their decision.

If you feel like they have misunderstood the issue, ask for clarification, and answer any questions they may have.

## Someone left a blocking comment on my pull request, and is taking a while to re-review my changes. What should I do?

This is a nuanced scenario that depends on how fast a team is accustomed to going, how fast it needs to go at this moment, and whether all team members are in agreement about the above.  As interesting as the answer is, it’s out of the scope of this post.

# Frequently Asked Questions (As The Reviewer)

## My comment doesn’t fall into any of these categories. What should I do?

Your comment likely does fall into one of these categories. If you feel that it does not, default to 🎨, as such a comment requires the least amount of work from the pull request author.

## My comment falls into multiple categories. What should I do?

Your comment would probably be better served with a single focus. For example, the following combinations can be simplified:

* ❔ + 🎨 — you likely cannot confidently propose a refactor when you have a related, unanswered question. Lead with a question, and propose a refactor later.
* ❔ + ❗️ — if you are not confident that the pull request can merge, you should always block
* 🎨 + ❗️ — decide whether the suggestion is blocking or not. It cannot be both.

## The pull request author is ignoring my 🎨 comments. How do I get them to listen to me?

You’ve given the pull request author the privilege to ignore these comments. If you feel like your comments require attention before merging, mark them accordingly: ❗️.

If you feel like your comments are non-blocking but should still be addressed, you should introspect about why you feel like that is the case. Perhaps the comments are indeed blocking, or your sense of what is blocking has drifted from the team’s.

## I want to mark my comment as blocking, but I do not want to be responsible for re-reviewing. What should I do?

If you believe that code is dangerous to merge, preventing it from doing so is one of the most important things you can do as an engineer. You should try to make time in your schedule to be a part of that process.

In rare cases, you may need to prevent a pull request from merging, but do not have time to re-review the pull request (i.e. reviewing a pull request the day before you go on vacation). In such cases, you should explicitly delegate that responsibility to someone else.E.g.:

```
❗️This line introduces an N+1 query. Have @eskfung confirm once it’s fixed.
```

## I want the pull request author to take my feedback seriously, but I do not want to mark it as blocking. What should I do?

One of the great advantages of this approach is that pull request authors do not have to guess as to what you think is important or not. You are not insulting their work by leaving a ❗️ comment, you are simply communicating how important you feel the issue is.

If you feel like your feedback is not being taken seriously, this may be a symptom of larger issues on the team, and should be addressed outside of the pull request process.

# Final Thoughts

At the end of the day, your goal as an engineer is to ensure your team understands which changes are acceptable for merging, and which changes are worth blocking. Your job is (probably) not to create an emoji glossary. I have been on teams that will smoothly alternate between annotating comments with emoji and annotating with text, like “Non-blocking comment:” or “Totally nitpicking, but…” Both approaches fulfill the same outcome of making a review less ambiguous. Experiment with your own strategy, as long as everyone understands and agrees with your team’s PR review culture.
