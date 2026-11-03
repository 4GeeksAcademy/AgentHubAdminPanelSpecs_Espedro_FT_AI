# AgentHub Admin Panel Specification

## Scope

Specify an admin panel for managing AgentHub platform activity, users, agents, skills, rental contracts, and execution errors. The panel contains the six sections below.

## Product and Admin User

AgentHub lets clients rent AI agents and combine reusable skills to support research, customer service, data analysis, content creation, and workflow automation. The platform administrator manages clients, agent configurations, the skill catalog, rental billing, and execution health across all clients.

## Implementation and Constraints

- The complete panel lives in `index.html`; open it directly in a browser or serve it with a static web server.
- HTML, Tailwind CSS via CDN, and vanilla JavaScript only. No custom CSS, framework, or backend.
- An internet connection is required to load Tailwind from its CDN.
- Sample data powers all six sections. Data edits last for the current page session; reloading restores sample records.
- Theme preference is saved in browser local storage. Hash-based navigation supports direct links and browser history.
- Dashboard billing metrics use the fixed November 2026 demo period. The weekly chart is an illustrative placeholder, not live analytics.
- Deleting users or skills that are still referenced by agents is blocked. Historical contract and error records are retained when agents are deleted.
- The dashboard CSV export contains all sample rental contracts, including historical ones.

## Reusable Component Inventory

| Component | Shared behavior |
| --- | --- |
| Sidebar | Persistent navigation to six sections, active indicator, mobile drawer. |
| Metric card | Label, icon, value, and contextual note. |
| Action dropdown | Per-record actions, outside-click and Escape dismissal. |
| Modal | Native dialog with focus management, close button, Escape, and backdrop dismissal. |
| Badge | Shared plan, status, and severity styling. |
| Collapsible skill list | Hidden initially, accessible expanded state, animated reveal, reduced-motion support. |
| Dark mode toggle | Applies Tailwind `dark:` utilities throughout the interface and saves the preference. |
| Listing table | Shared headers, row layout, horizontal overflow, and empty state. |
| Search and status filter | Search current-section records and filter supported listings by status. |
| Toast | Accessible feedback for completed actions and preference-storage errors. |

## Shared Interface

- Provide persistent sidebar navigation to Dashboard, User Management, Agent Management, Skills, Agent Contracts, and Error Log.
- Provide a top-bar toggle that switches the entire interface between light and dark mode using Tailwind `dark:` utilities.

## 1. Dashboard

Show four visible metric cards:

- Total revenue generated this month.
- Total discount and coupon losses.
- Number of active agents across all clients.
- Number of agents currently flagged as failing.

Below the metric cards, include a placeholder area for a weekly activity chart.

## 2. User Management

Show a table of all registered users with these columns:

- Name.
- Email.
- Plan.
- Status.

Each row has an action dropdown opened by a `⋮` button, with:

- **View detail:** Open a modal overlay displaying the full user record. The modal closes through a close button or by clicking the backdrop.
- **Delete.**

## 3. Agent Management

List all agents registered on the platform. Show each agent's name, owner, current status, and skills. Status values are active, inactive, or failing.

- Hide each agent's associated skills by default. An expand control reveals the full skill list with a smooth transition.
- Each agent has an action dropdown with **Configure** and **Delete**.
- **Configure** opens a modal displaying the agent's system prompt.

## 4. Skills

Show a catalog of available skills, where each skill includes:

- Name.
- Short description.
- Number of agents that currently have the skill enabled.

Include a brief in-panel explanation of what a skill means in the AgentHub platform context.

Each skill has an action dropdown with **View detail** and **Delete**.

## 5. Agent Contracts

Show a table of active and past rental contracts. Each row includes:

- Client.
- Rented agent.
- Contracted skills.
- Contract dates.
- Total amount paid.

Each row has an action dropdown. **View detail** opens a modal showing the full contract breakdown, including an itemized list of contracted skills and their individual prices.

## 6. Error Log

Show agent execution errors with each entry's:

- Timestamp.
- Agent name.
- Error type.
- Short description.

Use color-coded badges to visually categorize errors by type or severity.

Each entry has an action dropdown with:

- **View detail:** Open a modal displaying the full error trace.
- **Mark as resolved.**

## Acceptance Criteria

- The persistent sidebar provides navigation to all six sections.
- The top-bar theme toggle switches the entire interface between light and dark modes using Tailwind `dark:` utilities.
- The Dashboard displays all four required metrics and a weekly activity chart placeholder.
- User, agent, skill, contract, and error listings show every field specified for their section.
- Each required dropdown exposes its specified actions.
- User detail modals show the full user record and close with either the close button or backdrop click.
- Agent skills are hidden initially and expand with a smooth transition; Configure opens a modal with the system prompt.
- Contract detail modals include the full breakdown and individual prices for contracted skills.
- Error entries use color-coded type or severity badges, and error detail modals show the full trace.
