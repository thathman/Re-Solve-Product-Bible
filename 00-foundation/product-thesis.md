# Re:Solve Product Thesis

## Purpose

Re:Solve is a modular operating system for service businesses that need one coherent place to manage clients, digital properties, projects, commercial work, billing, confidential information, notifications, automation, AI-assisted operations, and integrations.

It is designed to replace fragmented operational workflows without pretending every specialist function should be rebuilt inside Re:Solve itself.

## Core Product Idea

Re:Solve owns business truth and operational context.

It should know:
- who the client is
- who their contacts are
- what properties and services they own or receive
- what work is in progress
- what is blocked
- what has been proposed, approved, contracted, billed, paid, renewed, or cancelled
- what requires staff or client attention
- what confidential information is shared
- what external systems are connected
- what happened, who did it, and when

Specialist systems remain specialist systems where that produces a better product. Re:Solve connects them through first-class connectors and exposes their useful context inside the OS.

## Product Position

Re:Solve is not:
- a generic dashboard template
- a CRM with a collection of unrelated add-ons
- a helpdesk replacement
- a payment processor
- a document-signing cryptography platform
- an accounting suite by default
- an AI wrapper around third-party products

Re:Solve is:
- a loaded operational workspace
- a client relationship system
- a property-centric service operations system
- a project and delivery system
- a commercial and billing system
- a secure client collaboration system
- a notification and automation platform
- an extensible plugin host
- a connector hub
- an API-first and MCP-capable system
- a responsive PWA for staff and clients

## Primary Product Surfaces

### Admin OS

The staff-facing operating environment. It is optimized for density, speed, cross-record context, operational awareness, and fast action.

### Client Portal

The client-facing operating environment. It is optimized for clarity, trust, approvals, visibility, self-service, collaboration, and mobile use.

These are two experiences over the same product model, permission system, event system, audit history, plugin system, connector system, and notification engine.

## Core Domains

Re:Solve should ultimately provide deeply integrated capabilities across:
- organisations and contacts
- CRM and opportunities
- properties and infrastructure context
- projects and delivery
- services and commercial records
- billing and operational finance
- secure vault and confidential file sharing
- files and documents
- knowledge
- notifications
- automations
- built-in AI
- reports and analytics
- plugins
- connectors
- API and MCP
- audit and security
- system health and administration

## Property-Centric Operating Model

A property is a first-class operational object representing something the organisation owns, operates, publishes, hosts, manages, sells through, or depends on.

Examples include:
- website
- journal
- OJS installation
- domain
- server
- hosting account
- store
- application
- API/service endpoint
- infrastructure component

Properties may have parent-child relationships.

Projects, support context, credentials, files, services, monitoring, incidents, renewals, and connector instances may attach to properties.

## Support Boundary

Chatwoot owns managed client support infrastructure, including:
- helpdesk conversations
- web chat on client properties
- support inboxes
- support teams and agents
- support knowledge
- Chatwoot's own AI engine

Re:Solve does not rebuild those functions.

Re:Solve stores and surfaces the business context around support, such as client, property, service entitlement, SLA, related project, incidents, analytics, and Chatwoot references.

## Communications Boundary

WhatsApp/Baileys is primarily used for operational communication between Re:Solve users and clients.

Examples include:
- ticket and status updates
- project updates
- approval reminders
- invoice and payment messages
- renewal reminders
- monitoring alerts
- credential requests
- general account-management communication

Client end-customer support remains a Chatwoot concern.

## AI Boundary

Re:Solve has its own built-in AI system for operational work such as:
- briefings
- drafting
- summaries
- search
- analysis
- record understanding
- controlled actions

Chatwoot AI remains separate. Re:Solve must not become a wrapper around Chatwoot's AI engine.

## Secure Vault Boundary

The Secure Vault is for controlled sharing of confidential information and files.

It may contain:
- passwords
- API keys
- credentials
- recovery codes
- confidential notes
- proposals
- contracts
- certificates
- sensitive documents
- protected files

Vault access must be permissioned, auditable, revocable, and capable of step-up authentication where appropriate.

## Extensibility Thesis

Re:Solve should be opinionated in core and extensible at the edges.

Core capabilities should not require plugins merely to function.

Plugins add business capabilities.

Connectors integrate external systems.

Payment providers are an explicit example: Re:Solve owns billing records and payment state, while payment providers are installed as plugins/connectors rather than hard-coded into core.

## API and AI Integration Thesis

Meaningful product functionality should be externally accessible through a documented API unless explicitly excluded for security or internal reasons.

Re:Solve should also expose a first-class MCP surface suitable for trusted integrations with AI and agent systems such as Claude, ChatGPT, Codex, OpenClaw/Hermes, and future tools.

API and MCP access must respect the same permissions, organisation isolation, property isolation, audit policy, and redaction rules as the UI.

## PWA Thesis

Responsive and installable behavior is a foundation requirement, not a post-launch enhancement.

Every major client-facing flow must be designed for phone, tablet, laptop, and desktop from the start.

The Admin OS must remain usable on smaller screens, even where highly complex workflows are optimized for larger displays.

## Design Thesis

Re:Solve should feel like a serious operating environment rather than a collection of SaaS cards.

The design should be:
- dense but calm
- fast to scan
- highly contextual
- deliberate about hierarchy
- responsive
- keyboard-friendly where appropriate
- accessible
- state-aware
- visually distinctive without sacrificing utility

Shared components and proven UI primitives should be preferred over inconsistent bespoke controls. shadcn/ui is a preferred foundation, with strong alternatives permitted where they materially improve the experience.

## Build Philosophy

The Product Bible may be exhaustive.

Implementation must not be.

The product is built in small, reviewable slices. Each slice should solve one bounded user flow or surface completely before the next area is introduced.

The existing Re-Solve repository is a source of product behavior, business logic, edge cases, and feature ideas. Its current technology choices are not automatically binding. Implementation should favor the current Lovable-compatible model while preserving product intent and future portability.

## Success Condition

Re:Solve succeeds when a service business can understand its clients, work, properties, finances, risks, communication, confidential information, and next actions from one coherent operating system without being locked into a monolithic dependency architecture.