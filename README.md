# Claude Code Configuration

Personal Claude Code configuration for multi-project development workflow.

## Files

- `CLAUDE.md` - Global instructions and preferences for all projects
- `commands/` - Custom Claude commands for common workflows
  - `fix-github-issue.md` - Automated GitHub issue fixing workflow
  - `give-me-a-commit-message.md` - Commit message generator with conventional format
- `agents/` - Documentation of available Claude Code agents

## Setup

1. Clone this repository to `~/.claude/`
2. Claude Code will automatically use these global settings across all projects

## Sync Between Machines

This repository allows syncing Claude Code configuration between multiple development machines through git.

## Available Agents

> **⚠️ IMPORTANT NOTICE**
> 
> The agents documented below are from **[Contains Studio](https://github.com/contains-studio/agents)**, a premium collection of specialized AI agents designed for rapid app development within 6-day cycles.
> 
> **All rights and ownership of these agents belong to Contains Studio.** They are not part of the default Claude Code installation. This documentation is for reference only.
> 
> For more information, please visit: https://github.com/contains-studio/agents

### Development Agents

#### rapid-prototyper
Quickly create application prototypes, MVPs, or proof-of-concepts within 6-day development cycles. Specializes in scaffolding projects and building functional demos.

#### frontend-developer
Build user interfaces, implement React/Vue/Angular components, handle state management, and optimize frontend performance.

#### backend-architect
Design APIs, build server-side logic, implement databases, and architect scalable backend systems.

#### mobile-app-builder
Develop native iOS or Android applications, implement React Native features, and optimize mobile performance.

#### ai-engineer
Implement AI/ML features, integrate language models, build recommendation systems, and add intelligent automation.

#### devops-automator
Set up CI/CD pipelines, configure cloud infrastructure, implement monitoring systems, and automate deployment processes.

### Testing & Quality Agents

#### test-writer-fixer
Write new tests, run existing tests, analyze failures, and fix them while maintaining test integrity. Triggered after code modifications.

#### test-results-analyzer
Analyze test results, synthesize test data, identify trends, and generate quality metrics reports.

#### performance-benchmarker
Comprehensive performance testing, profiling, and optimization recommendations.

#### api-tester
Comprehensive API testing including performance testing, load testing, and contract testing.

### Project Management Agents

#### sprint-prioritizer
Plan 6-day development cycles, prioritize features, manage product roadmaps, and make trade-off decisions.

#### studio-producer
Coordinate across multiple teams, allocate resources, and optimize studio workflows.

#### project-shipper
Coordinate launches, manage release processes, and execute go-to-market strategies.

#### experiment-tracker
Track A/B tests, feature experiments, and iterative improvements within development cycles.

#### workflow-optimizer
Optimize human-agent collaboration workflows and analyze workflow efficiency.

### Marketing & Growth Agents

#### tiktok-strategist
Create TikTok marketing strategies, develop viral content ideas, plan campaigns, and optimize for TikTok's algorithm.

#### app-store-optimizer
Prepare app store listings, research keywords, optimize app metadata, and improve conversion rates.

#### trend-researcher
Identify market opportunities, analyze trending topics, research viral content, and understand emerging user behaviors.

#### feedback-synthesizer
Analyze user feedback from multiple sources, identify patterns, synthesize insights, and prioritize feature development.

### Design & UX Agents

#### ui-designer
Create user interfaces, design components, build design systems, and improve visual aesthetics.

#### brand-guardian
Establish brand guidelines, ensure visual consistency, manage brand assets, and evolve brand identity.

#### ux-researcher
Conduct user research, analyze user behavior, create journey maps, and validate design decisions.

#### visual-storyteller
Create visual narratives, design infographics, build presentations, and communicate complex ideas through imagery.

#### whimsy-injector
Add delightful, playful elements to user experiences. Automatically triggered after UI/UX changes.

### Support & Operations Agents

#### legal-compliance-checker
Review terms of service, privacy policies, ensure regulatory compliance, and handle legal requirements.

#### analytics-reporter
Analyze metrics, generate insights from data, create performance reports, and make data-driven recommendations.

#### support-responder
Handle customer support inquiries, create support documentation, set up automated responses, and analyze support patterns.

#### finance-tracker
Manage budgets, optimize costs, forecast revenue, and analyze financial performance.

#### infrastructure-maintainer
Monitor system health, optimize performance, manage scaling, and ensure infrastructure reliability.

### Utility Agents

#### tool-evaluator
Evaluate new development tools, frameworks, or services. Perform rapid tool assessment and comparative analysis.

#### studio-coach
Elite performance coach for all other agents. Ensures agents operate at highest level while maintaining composure and excellence.

#### joker
Lighten the mood, create funny content, and add humor to any situation with dad jokes and programming puns.

#### general-purpose
General-purpose agent for researching complex questions, searching for code, and executing multi-step tasks.

### Specialized Agents

#### statusline-setup
Configure the user's Claude Code status line setting.

#### output-mode-setup
Create a Claude Code output mode.