# Hi, I'm Ankit

I spent most of my career moving regulated data around safely, first for planes, then for medicine. Doctorate in deep learning, two startup exits, engineering orgs of about a hundred people. None of it prepared me for a veterinary clinic's filing system, so I'm fixing that instead.

## Building now

**[Yosemite Crew](https://github.com/YosemiteCrew/Yosemite-Crew)** - an open-source operating system for animal health. Scheduling, medical records, invoicing, inventory: the plumbing a clinic actually runs on. AGPLv3, with web, desktop and mobile apps built from one TypeScript monorepo.

**[openrunic](https://github.com/YosemiteCrew/openrunic)** - the same idea pointed at human health. Early, and public since the first commit.

## Where the work lives

Most of my code is in the [YosemiteCrew](https://github.com/YosemiteCrew) org, not in this account's repo list. Start with the [Yosemite-Crew commit history](https://github.com/YosemiteCrew/Yosemite-Crew/commits?author=aupyay) and the pull request reviews; I ship and review daily. Every pull request passes SonarCloud with 95 percent coverage on new code and zero new issues, plus security scanning and a full typed monorepo build, before it merges.

One housekeeping note: this account is younger than my career. I lost access to my older GitHub profiles, and the work that lived on them. If you come across my prior projects out in the community, let me know.

## How this gets built

Most of the code here is written by AI agents, deliberately and at scale. My job is the part that survives contact with production: choosing what gets built, drawing the system boundaries, and building the machinery that catches what agents get wrong. The rules they work under are versioned in the repo itself: [AGENTS.md](https://github.com/YosemiteCrew/Yosemite-Crew/blob/main/AGENTS.md) is a hierarchy of operating instructions that Codex, Claude Code and friends load before touching a workspace.

An agent will happily merge anything that passes, so what passes is where I spend my judgment. All of it is public: [PR governance](https://github.com/YosemiteCrew/Yosemite-Crew/blob/main/.github/workflows/pr-governance.yml) and a [promotion guard](https://github.com/YosemiteCrew/Yosemite-Crew/blob/main/.github/workflows/promotion-guard.yml) between dev and main, [secret scanning](https://github.com/YosemiteCrew/Yosemite-Crew/blob/main/.github/workflows/secret-scan.yml), [dependency review](https://github.com/YosemiteCrew/Yosemite-Crew/blob/main/.github/workflows/dependency-review.yml), [supply-chain scans with SBOMs](https://github.com/YosemiteCrew/Yosemite-Crew/blob/main/scripts/security/supply-chain.sh), pinned transitive dependencies [checked against advisories in CI](https://github.com/YosemiteCrew/Yosemite-Crew/blob/main/scripts/ci/check-override-advisories.mjs), [container](https://github.com/YosemiteCrew/openrunic/blob/main/.github/workflows/container-scan.yml) and [infrastructure scans](https://github.com/YosemiteCrew/openrunic/blob/main/.github/workflows/iac-scan.yml), an [OSSF scorecard](https://github.com/YosemiteCrew/openrunic/blob/main/.github/workflows/scorecard.yml), [attested releases](https://github.com/YosemiteCrew/openrunic/blob/main/.github/workflows/release-attest.yml), and a [workflow audit](https://github.com/YosemiteCrew/openrunic/blob/main/.github/workflows/workflow-audit.yml) so the CI cannot quietly drift either. Health data gets its own tripwire: [CI fails when PHI turns up where it should not](https://github.com/YosemiteCrew/openrunic/blob/main/.github/workflows/phi-guard.yml).

The judgment calls are on the record too. A provider-independent auth boundary before the SuperTokens migration ([#1763](https://github.com/YosemiteCrew/Yosemite-Crew/pull/1763)). Stripe direct charges so the clinic, and never the platform, is the merchant of record ([#1680](https://github.com/YosemiteCrew/Yosemite-Crew/pull/1680)). Tenant scope derived from resources instead of trusted from the caller ([#1860](https://github.com/YosemiteCrew/Yosemite-Crew/pull/1860)). A pet passport whose clinical records carry attestation ([#1675](https://github.com/YosemiteCrew/Yosemite-Crew/pull/1675)).

openrunic ships an agent of its own, so the governance ships as code: the [agent loop](https://github.com/YosemiteCrew/openrunic/tree/main/packages/agent) enforces approval gating, tenant scoping, budget caps and audit emission, and the [clinical safety package](https://github.com/YosemiteCrew/openrunic/tree/main/packages/clinical-safety) screens prescriptions for allergies and cross-sensitivities before a suggestion reaches a human. Agents type faster than I ever will. Not one has asked me whether the backup restores; [there is a job for that too](https://github.com/YosemiteCrew/openrunic/tree/main/packages/ops).

## Stack

TypeScript end to end, in a pnpm and Turborepo monorepo. Next.js and React on the web, React Native on mobile, Electron on desktop. APIs in Express and Hono. Postgres through Prisma and Supabase with row-level security, Redis and BullMQ for queues, Socket.IO for realtime.

The clinical side speaks the standards nobody sees and everybody depends on: FHIR, HL7v2, C-CDA and CDS Hooks. Around them: Stripe Connect for payments, Firebase for push, AWS for storage and email, infrastructure as code with CDK, Docker images for self-hosting.

Tested with Jest, Playwright and Storybook. Gated by SonarCloud, CodeQL, dependency review, secret scanning and supply-chain checks. Boring on purpose.

![TypeScript](https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white)
![Next.js](https://img.shields.io/badge/Next.js-000000?style=for-the-badge&logo=nextdotjs&logoColor=white)
![React](https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)
![React Native](https://img.shields.io/badge/React_Native-20232A?style=for-the-badge&logo=react&logoColor=61DAFB)
![Electron](https://img.shields.io/badge/Electron-2B2E3A?style=for-the-badge&logo=electron&logoColor=9FEAF9)
![Node.js](https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=nodedotjs&logoColor=white)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=for-the-badge&logo=postgresql&logoColor=white)
![Prisma](https://img.shields.io/badge/Prisma-2D3748?style=for-the-badge&logo=prisma&logoColor=white)
![pnpm](https://img.shields.io/badge/pnpm-F69220?style=for-the-badge&logo=pnpm&logoColor=white)
![Jest](https://img.shields.io/badge/Jest-C21325?style=for-the-badge&logo=jest&logoColor=white)
![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?style=for-the-badge&logo=githubactions&logoColor=white)
![Express](https://img.shields.io/badge/Express-000000?style=for-the-badge&logo=express&logoColor=white)
![Hono](https://img.shields.io/badge/Hono-E36002?style=for-the-badge&logo=hono&logoColor=white)
![Supabase](https://img.shields.io/badge/Supabase-3FCF8E?style=for-the-badge&logo=supabase&logoColor=white)
![Redis](https://img.shields.io/badge/Redis-FF4438?style=for-the-badge&logo=redis&logoColor=white)
![Socket.IO](https://img.shields.io/badge/Socket.IO-010101?style=for-the-badge&logo=socketdotio&logoColor=white)
![Stripe](https://img.shields.io/badge/Stripe-635BFF?style=for-the-badge&logo=stripe&logoColor=white)
![Firebase](https://img.shields.io/badge/Firebase-DD2C00?style=for-the-badge&logo=firebase&logoColor=white)
![AWS](https://img.shields.io/badge/AWS-232F3E?style=for-the-badge&logo=amazonwebservices&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)
![FHIR](https://img.shields.io/badge/FHIR-E8340C?style=for-the-badge)
![HL7v2](https://img.shields.io/badge/HL7v2-CC0000?style=for-the-badge)
![C-CDA](https://img.shields.io/badge/C--CDA-4A5568?style=for-the-badge)
![CDS Hooks](https://img.shields.io/badge/CDS_Hooks-1976D2?style=for-the-badge)
![Turborepo](https://img.shields.io/badge/Turborepo-000000?style=for-the-badge&logo=turborepo&logoColor=white)
![Playwright](https://img.shields.io/badge/Playwright-2EAD33?style=for-the-badge)
![Storybook](https://img.shields.io/badge/Storybook-FF4785?style=for-the-badge&logo=storybook&logoColor=white)
![SonarCloud](https://img.shields.io/badge/SonarCloud-F3702A?style=for-the-badge&logo=sonarqubecloud&logoColor=white)
![Docusaurus](https://img.shields.io/badge/Docusaurus-3ECC5F?style=for-the-badge&logo=docusaurus&logoColor=white)

## Scoreboard

[![GitHub followers](https://img.shields.io/github/followers/aupyay?style=for-the-badge&logo=github&label=Followers)](https://github.com/aupyay?tab=followers)
[![Yosemite Crew stars](https://img.shields.io/github/stars/YosemiteCrew/Yosemite-Crew?style=for-the-badge&logo=github&label=Yosemite%20Crew%20stars)](https://github.com/YosemiteCrew/Yosemite-Crew)
![Profile views](https://komarev.com/ghpvc/?username=aupyay&style=for-the-badge)

<picture>
<source media="(prefers-color-scheme: dark)" srcset="https://streak-stats.demolab.com?user=aupyay&theme=dark&hide_border=true&background=00000000">
<img alt="GitHub streak" src="https://streak-stats.demolab.com?user=aupyay&hide_border=true">
</picture>

## Elsewhere

[yosemitecrew.com](https://yosemitecrew.com) · [YosemiteCrew on GitHub](https://github.com/YosemiteCrew) · [LinkedIn](https://www.linkedin.com/in/aupyay)
