---
layout: post
title: "The Intent Gap in Software Requirements"
date: 2026-01-18
categories: [blog, software-engineering]
tags: [estimation, requirements, knowledge-management, ai, tacit-knowledge]
excerpt: "Why software estimation fails despite better tools: Requirements capture the 'what' while losing the 'why,' creating a Knowledge Transfer Tax that compounds when using historical data. As AI enters development, we face a critical choice."
---

# The Intent Gap in Software Requirements

Your team estimated the new payment integration at three weeks.

The rationale was solid. You built a similar OAuth flow last quarter. Same tech stack. Same patterns. The requirements looked almost identical.

Six weeks later, you're still debugging edge cases no one documented.

What happened?

This isn't a story about poor planning or incompetent teams. It's a story that plays out in engineering organizations everywhere, regardless of how sophisticated their estimation processes are.

The problem runs deeper than methodology. It's an information theory problem. And as generative AI enters software development, we're at a critical inflection point: we're about to make this problem either dramatically better or significantly worse.

## The Comparable Fallacy

Here's the paradox: Teams have more historical data than ever before. JIRA tickets, git histories, velocity metrics, and story points refined across dozens of sprints. Yet estimation accuracy hasn't improved.

Research from IEEE Transactions on Software Engineering shows that despite decades of methodological refinement, software projects still routinely miss estimates by 50% or more. Magne Jørgensen's meta-analyses of estimation methods reveal a stubborn truth: whether you use story points, function points, or sophisticated parametric models, the accuracy ceiling remains frustratingly low.

Why?

Because we're comparing incomplete blueprints.

Consider two projects, both documented as "implement user authentication":

**Project A:** Three days. The team integrated an existing OAuth provider, configured the callbacks, and called it done.

**Project B:** Thirty days. The team built custom cryptographic protocols to meet regulatory compliance, integrated with a legacy identity system that had undocumented quirks, and navigated organizational politics around data sovereignty.

Both requirements say the same thing on paper. But one required 10x the effort.

The requirements captured the "what" (implement user authentication). They missed the "why" that actually drove the work: regulatory constraints, legacy system archaeology, team expertise gaps, stakeholder negotiations.

As Fred Brooks observed in "No Silver Bullet," some complexity is essential, not accidental. You can't engineer it away with better processes. The context that makes Project B harder than Project A is intrinsic to the problem itself.

## What Actually Gets Lost

When a project ends and the documentation goes into the archive, what disappears?

**Organizational context.** The political constraints. The fact that Legal blocked the first three approaches. The stakeholder who changed their mind twice about encryption requirements.

**Technical archaeology.** The legacy API that returned inconsistent data formats. The platform limitation discovered three days in. The database quirk that forced a complete redesign.

**Team expertise.** That Sarah knew this codebase inside-out. That Alex could debug the obscure JWT validation issue in ten minutes because they'd seen it before. That the team had built shared mental models over months of working together.

**Decision rationale.** Why you chose approach A over B. What you tried that failed. The trade-offs you consciously made. The shortcuts you deliberately didn't take.

**Negative space.** What you deliberately didn't build. The features you scoped out. The constraints you worked around instead of solving.

This isn't laziness. Some knowledge simply can't be written down efficiently. When you're in the middle of solving a problem, you're swimming in context. When you're documenting it afterward, you're trying to compress hours of nuanced decision-making into a few paragraphs.

Something has to give. And what gives is the intent: the "why" behind the "what."

## The Theory: Tacit vs. Explicit Knowledge

There's a reason documentation fails to capture intent. It's not a process problem we can fix with better templates.

In 1995, Ikujiro Nonaka and Hirotaka Takeuchi published "The Knowledge-Creating Company," introducing a framework that explains why. Their SECI model describes how knowledge moves through four modes: Socialization, Externalization, Combination, and Internalization.

The critical insight: Not all knowledge can move from tacit to explicit.

**Tacit knowledge** is what you know through experience. It's context-dependent, often non-verbal, embedded in practice. When you've worked on a codebase for months, you develop an intuition for where bugs hide. You know which parts of the system are fragile. You understand the unwritten rules about how things work.

**Explicit knowledge** is what you can write down. Documentation. Requirements. Code comments.

The externalization bottleneck happens when you try to convert tacit knowledge into explicit knowledge. Some things just don't translate.

Jean Lave and Etienne Wenger's research on situated learning explains why "being there" matters so much. Learning (and knowledge) happens in context, embedded in practice. When you estimate based on historical data, you're trying to extract lessons from knowledge that was fundamentally situated in a specific time, place, team, and problem context.

This is why experienced teams estimate better. Not because they're smarter or more disciplined. Because they have direct access to tacit knowledge about the system, the team dynamics, the hidden constraints. They bypass the translation problem entirely.

## The Knowledge Transfer Tax

Now here's where it compounds.

Every time knowledge transfers from one context to another, it loses fidelity. I call this the Knowledge Transfer Tax.

Map the chain:

Original team → Documentation → Database → New team → AI tools → Estimation model

Each hop drops context. Each translation from tacit to explicit loses nuance. Each summarization loses rationale.

When the original team documents their work, maybe 70% of the decision context makes it into the writeup. When that documentation gets entered into JIRA, maybe 50% survives. When a new team reads those tickets months later, they extract perhaps 30% of the original context. When an AI tool analyzes that data to generate estimates, it's working with a fraction of what actually mattered.

This explains the experience advantage that's so frustrating to quantify. Veterans don't have better estimation models. They have fewer hops in the knowledge transfer chain. They were there. They have direct access to the tacit layer that never made it into documentation.

Brooks called this "conceptual integrity": the original designer holds a complete mental model. Every transfer fragments that model.

Think of it like comparing architectural blueprints for two buildings without knowing that one was built on bedrock and the other on a swamp. The blueprints look identical. The effort required is completely different. The critical context is invisible on paper.

## The AI Inflection Point

Now we're introducing generative AI into this system.

And here's where it gets interesting and uncertain.

### Two Possible Futures

**The optimistic scenario:** LLMs with large context windows can ingest entire codebases, years of issue history, pull request discussions, design documents, Slack conversations. They could theoretically preserve more context than any human-written summary ever could.

Retrieval-Augmented Generation (RAG) systems could reconstruct intent by connecting scattered pieces of context that humans would never manually link. The AI becomes organizational memory that doesn't forget. It doesn't lose tacit knowledge when engineers leave. It can surface relevant context from five years ago that's still applicable today.

In this world, AI reduces the Knowledge Transfer Tax. It preserves the "why" alongside the "what." Estimation improves because the AI has access to richer context than any historical database we've built before.

**The pessimistic scenario:** AI-generated requirements look complete but hide new forms of assumptions. The black box problem compounds: the LLM makes connections that humans don't understand. It hallucinates plausible-sounding context that isn't real.

Teams start trusting AI estimates without understanding the hidden gaps. When the AI says "this is similar to Project X," what does "similar" mean? Does the model understand the difference between OAuth integration and custom cryptography? Or is it pattern-matching on surface features while missing essential complexity?

We create a new form of tacit knowledge: "The AI knows why, but we don't."

The estimates might even be accurate, but if we can't inspect the reasoning, we can't improve it. We can't identify where the model is making unfounded assumptions. We can't transfer the learning to new team members.

In this world, AI increases the Knowledge Transfer Tax. It adds another layer of opacity between intent and documentation.

## The Critical Questions We Must Answer

These aren't academic questions. Engineering organizations are making decisions about AI-assisted development right now. The choices we make will determine which scenario we get.

- **Can current LLMs handle project-specific context?** When you give GPT-4 or Claude your codebase and requirements, can they actually reconstruct the intent that isn't documented? Or do they hallucinate plausible-sounding but incorrect context?

- **What's the Knowledge Transfer Tax in quantitative terms?** Can we measure how much efficiency we lose when knowledge moves from experienced team to documentation to new team? What percentage of decision context actually survives that journey?

- **Does AI-generated content preserve or destroy the "why"?** When teams use AI to draft requirements or generate estimates, are we capturing more context or less? Are we making it easier to understand intent, or harder?

- **What organizational practices help?** Do we need to invest in intent-preserving documentation before scaling AI-assisted development? What does that even look like? Architecture Decision Records? "5 Whys" documentation? Constraint mapping?

- **Are we measuring the right things?** Should we evaluate AI tools by asking "does this preserve context" instead of just "is the estimate accurate"?

The window to answer these questions is shrinking. Teams are already using AI for estimation, for requirements generation, for code review. We're making the bet implicitly even if we're not making it explicitly.

## Reframing the Problem

Here's what changes when you see estimation as an information preservation problem instead of a methodology problem:

You stop looking for the perfect estimation technique. Story points vs. t-shirt sizing vs. function points: none of them matter if the underlying context is missing. No measurement system can compensate for lost information.

You start asking different questions. Not "how do we estimate better?" but "how do we preserve intent?" Not "which AI tool is most accurate?" but "which AI tool helps us understand the 'why'?"

You recognize that the real opportunity with AI isn't about automating estimation. It's about whether we can use AI to reduce the Knowledge Transfer Tax: to capture and preserve the tacit knowledge that normally gets lost.

But that only works if we're intentional about it.

If we blindly adopt AI-generated requirements and AI-assisted estimation without understanding what context is being preserved or lost, we risk building a new generation of black box systems. Requirements that look complete on the surface but hide assumptions that will surprise us six weeks into implementation.

The Knowledge Transfer Tax will go up, not down.

## The Choice Ahead

In an AI-assisted development world, are we about to solve the Knowledge Transfer Tax, or compound it?

The answer depends on choices we make now.

Do we treat AI as a documentation tool that helps preserve context? Or as a productivity tool that generates outputs we don't fully understand?

Do we invest in capturing intent alongside requirements? Or do we assume the AI will figure it out?

Do we measure success by estimation accuracy? Or by how well we understand the reasoning behind the estimates?

Your organization is making these choices whether you realize it or not. Every time you use an AI coding assistant. Every time you adopt an AI-powered estimation tool. Every time you let an LLM generate requirements.

The question isn't whether to use AI. That ship has sailed.

The question is: Are you using it to preserve the "why," or just generate more "what"?

Here's where to start: Pick one project your team completed in the last quarter. Read the requirements documentation. Then talk to someone who actually built it. Ask them what's not in the documentation: what context got lost, what assumptions were made, what constraints shaped the work.

That gap you discover? That's the Knowledge Transfer Tax. And understanding it is the first step toward reducing it.

Think about that the next time a three-week estimate turns into six weeks of debugging undocumented edge cases.

What context got lost? And could AI have helped preserve it, or did it make the problem worse?
