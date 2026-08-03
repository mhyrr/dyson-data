---
title: The Karpathy-Inspired System That Makes Codex More Reliable
channel: Reza Hey
published: 2026-07-28T06:00:38Z
url: https://youtube.com/watch?v=RHHa3K6C3LI
video_id: RHHa3K6C3LI
source: people_search
person: Andrej Karpathy
fetched: 2026-08-03T18:33:07.525383+00:00
segments: 0
---

# The Karpathy-Inspired System That Makes Codex More Reliable

**Channel:** Reza Hey  
**Published:** 2026-07-28T06:00:38Z  
**URL:** https://youtube.com/watch?v=RHHa3K6C3LI  

---

An AI system can be remarkably capable and
still optimize the wrong problem. Andrej Karpathy illustrated that gap with a
deceptively simple scenario. Your car needs washing, the car washes only a short
distance away, and a model recommended walking because walking is efficient. It
notices the distance but misses the relationship that defines the task. The
car itself has to arrive. That small failure explains a much larger one. Give
an agent an underspecified assignment and it can produce an impressive answer to the
wrong question. More intelligence does not rescue context you never supplied.
Karpathy has argued for developing a detailed specification with an agent
instead of treating a high-level plan as the finish line. The source that inspired
this tutorial organized this idea into three practical layers. The specification,
the verifier, and the working environment. We will turn the first layer into a
decision-ready plan and the second into visible evidence. And the third into
persistent instructions, reusable skills, connected tools, and the real permission
boundaries. I'm not claiming that Karpathy formally named this framework, endorsed
this workflow, or promised a 10 times improvement. This is a Codex-native
implementation inspired by the underlying principles. Your understanding must shape
the system around the agent. I'm recording in the ChatGPT desktop app with Codex
selected. Work mode in ChatGPT shares the same core agent, but Codex exposes the
local project, terminal, git review, and developer controls needed for these
demonstrations. By the end, you will know what Codex can do directly, what requires
setup, and what the evidence does and does not prove. Suppose you tell Codex, build
me an end-of-month report. Who reads it? What decision should it support? Which
numbers matter? What format already works? And what makes the result
unacceptable? If those decisions are missing, Codex still has to produce
something. The output may look polished while being completely misaligned. So do
not measure progress by how quickly the agent starts. Measure it by how few
important assumptions survive into the build. For ambiguous work, Codex has a
plan mode. It can inspect available code context, ask clarifying questions, and
produce a plan before implementation. You can also explicitly ask it to interview
you. The goal is not merely to create a plan. The goal is to expose decisions
while changing them is still cheap. So I have opened the fictional client dashboard
project as a local chat and I am switching to plan mode because I want decisions, not
implementations. The project brief describes the rough assignment. The
account data shows what information is actually available. It is a small
fictional data set, 12 accounts with revenues, health, open risk, and last
contact fields. And an approval report gives Codex a structural reference. The
prompt authorizes Codex to inspect those materials, ask five decision-changing
questions, and produce the final plan. It explicitly prohibits file changes. Watch
the questions. Codex should make me choose the audience, the decision this dashboard
supports, the ranking method, the allowed data, and the definition of done instead
of quietly choosing those things itself. After the fifth answer, I'm checking the
plan for the requested headings. Then I'm opening the terminal and running git
status. The empty result and empty review panel prove that we clarified the work
without starting implementation. Plan mode exposes assumptions. It does not decide
the business goal or guarantee that the plan is correct. When you review a plan,
look for three warning signs. A decision disguised as a detail, an acceptance
criterion that cannot be observed, and a checkpoint containing several risky
changes. Send those back before building. Then make the work smaller. The second
project divides the dashboard into three explicit checkpoints. I'm using a local
chat in the default Codex mode because this time I'm authorizing an
implementation, but only checkpoint 1. The brief defines the outcome. The boundaries
file separates the stages. The existing code shows the starting point. Checkpoint
1 loads those same 12 local records from JSON into existing table. And the
acceptance script gives the first checkpoint an observable test. The prompt
asks Codex to describe all three stages but authorizes only the account table.
Summary cards, ranking logic, and mobile stylings are explicitly out of scope. Now
I'm checking the terminal for the checkpoint 1 pass message. In the review
panel, I'm looking for the table loading change and confirming that no later stage
work slipped into the diff. Finally, Codex stops at awaiting checkpoint 1 review.
That stop is useful workflow discipline. It is not a security boundary. I still
need to inspect the workflow before authorizing the next checkpoint. Once the
target is clear, decide what evidence would convince you that the result works.
For code, that might include tests, linting a reviewed diff, and the feature working
in a rendered interface. For a report, it might include required sections,
calculation checks against source data, and comparison with an approved example.
Do not let finished mean Codex said it was finished. With verification as a tiny
evidence table, name the claim, name the check, record the results, and state what
was not covered. That prevents a test command, a screenshot, and a vague
statement of confidence from blending into an impressive looking but useless
paragraph. This project contains one narrow visual
bug, two action links fit on desktop but need to stack on a small screen. I'm using
a local Codex chat because this demonstration combines file edit, an
automation test, and a rendered browser check. The task file defines the bug. The
style sheet is only an authorized implementation file, and the prompt
prohibits changes to the desktop structure, text colors, and the
JavaScript. First, I'm checking the terminal for the mobile acceptance pass
message. Next, the built-in browser shows the page at 1280 pixels and 390 pixels. On
desktop, the actions remain side-by-side. On mobile, they stack without horizontal
overflow, and both labels remain visible. Finally, the review panel should contain
only the scoped style sheet change. Codex reports separate evidence for the
automation check, desktop observation, and a mobile observation. If the browser is
unavailable, and I show the supplied screenshots, they are pre-verified
reference screenshots, not evidence from the live run. This proves the local host
behavior we actually inspected. It does not prove every viewport, an authenticated
state, or production behavior. The same rule applies to
deployment checks. A public health endpoint, approved command, or connected
tool can raise confidence. One green response does not prove the entire
deployment is correct. You can also request a separate review or specialized
sub-agents for areas such as security, test gaps, and maintainability, but a
second agent is not automatically independent or correct, and parallel
writers can conflict. Use critics when disagreement is informative. Use
deterministic checks where a machine can measure the results. And be careful with
the performance claims. OpenAI does not promise that the feedback loop will always
double quality and make anyone 10 times faster. Measure those outcomes in your own
workflow. If you want practical Codex workflows with visible proof and honest
limitations, subscribe. I really appreciate it. The next lesson will build
this into a reusable workspace from an empty folder. The first two layers need
somewhere durable to live. Start with AGENTS.md file. Codex reads supported
instructions files before it begins work. You can keep personal defaults globally,
shared expectations in project, and more specific guidance near subdirectory. This
is where you record important commands, conversations, constraints, and required
checks. I'm operating a genuinely fresh local chat so Codex discovers the project
instructions at the beginning of the run. AGENTS.md says that after changing the
sample page, Codex must run a smoke check and report the complete results. My prompt
authorizes the subtitle edit, and prohibits every other content or style
change. Notice that I do not mention testing. Now watch the terminal. Codex ran
the smoke checks because the project instructions required it, not because I
repeat it in a prompt. The review panel shows the only subtitle change and the
final report includes the passing smoke results. That proves the instruction was
discovered and followed in this run. AGENTS.md file is durable guidance, not an
operating system security boundary. Keep it short and operational. Put specialized
procedures somewhere better suited for repeatable workflows. That brings us to
the skills. A Codex skill is a reusable workflow built around a SKILL.md file with
optional scripts and references. This project contains a release note checker.
The skill defines the procedure that release notes provide the subject. The
policy supplies the standards and the output file makes the results inspectable.
I will show it twice in the fresh local chat. First, I explicitly select the
skill. Then I reset the project and describe the same job without naming it so
we can observe implicit matching. This skill writes the structured review, flags
the unsupported performance claims and missing migration guidance and runs the
repository check. The review panel should show the change only to the output file.
If implicit invocation is available, Codex select the same skill because the request
matches the description. Success shows that the work was selected and followed.
It does not guarantee that every judgment inside the review is correct. Local skills
are useful for one project or one person. When you want to distribute them or bundle
them with connectors or MCP configurations or hooks, the installable package is a
plugin. Codex can also read organized workspace files, use approved plugins or
MCP servers and optionally use local memories. Called as context and retrieval,
not model training, local Codex memories are experimental and off by default.
Required team rules still belong in checked-in guidance. Finally, separate advice from
enforcement. This disposable project demonstrates three different control
layers. AGENTS.md contains written guidance. The protected note file makes
the distinction visible. Being told not to edit a file is guidance, not file system
enforcement. The sandbox and permissions profile define technical access and an
experimental command rule describes one forbidden command prefix. I'm using a
local chat with workspace scoped permissions. The prompt authorizes one
read only network command and prohibits file change. Codex pauses for approval
before network access. I'm denying the request because the approval gate, not the
network results, is evidence we need. Some setups route eligible approvals to an
automated reviewer. That changes who evaluate the escalations. It does not
expand the sandbox or enable network access by itself. Next, I'm running the
policy checker against the supplied rule. It reports forbidden for the harmless curl
example without installing the rule. GateStatus remains empty. That visibly
separates prompt guidance, sandbox, and approval controls, and command prefix
rule. The rule is experimental and command oriented. It is not a universal file
policy engine. Hooks provide another extension point. They can observe many
local tool calls and pre-tool-use hook can block or rewrite supported calls, but a
specialized tool path can opt out of the default hook path. Treat hooks as trusted,
tested guardrails, not as unbypassable folder firewalls. For enforceable file
system boundaries, use an appropriate sandbox or permission profile. Here is the
hierarchy to remember. Put one-off direction in the prompt. Put durable
project behavior in AGENTS.md. Put repeatable procedures in skills. Use
approved plugins or MCP tools for live systems. Use permission profiles and
sandboxing for access boundaries, approvals for consent gates, and rules or
hooks only with their documented scope. The Karpathy-inspired idea underneath this
system is not the agent should replace your understanding. Your understanding has
to shape the system around the agent. Before the work, ask yourself, have we
made important decisions or are we asking Codex to guess? During the work, ask what
evidence will show that each checkpoint is correct. Across future work, ask which
lessons belong to the project, which belong in the reusable skills, and which
require an enforceable boundary. Codex can help you plan, execute, test, review,
and reuse what works, but it cannot decide what your business should value, and it
cannot turn an unmeasured assumption into a truth. Your advantage is not merely
having an agent, it is building a clear decision process around the agent and
refusing to confuse output with proof. Subscribe and go for the next one, where
we will build a reusable Codex workspace with project instructions and first
skills, verification commands, and safe permissions from the ground up. See you on
the next one, thank you for watching.
