# Notion Workspace

## Workspace Details

**Workspace Name:** `[YOUR_NOTION_WORKSPACE_NAME]`

**Team:** FL4LL

**Notion URL:** `https://www.notion.so/[WORKSPACE_ID]`

## Databases

### 1. Tasks / Roadmap

**Purpose:** Track Sheahaircare features, bugs, launches

**Schema:**
- Title (Task name)
- Status (Todo / In Progress / Done / Blocked)
- Priority (P0 / P1 / P2)
- Assignee
- Due date
- Related issue (link to GitHub)

### 2. Knowledge / Docs

**Purpose:** Vault architecture, system design, API docs

**Schema:**
- Title (Doc name)
- Category (Architecture / API / Onboarding / Decision)
- Status (Draft / Published / Archived)
- Last updated
- Owner

### 3. Customers / Users (optional CRM)

**Purpose:** Track users, feedback, support requests

**Schema:**
- Name
- Email
- Signup date
- Status (Active / Churned / Prospect)
- Feedback / Notes
- Last contacted

## API Integration

**Notion API Token:** `[GET_FROM_NOTION_SETTINGS]`

**How to get it:**
1. Go to [Notion Integrations](https://www.notion.so/my-integrations)
2. Create new integration
3. Copy the "Internal Integration Token"
4. Store in `.env.local` as `NOTION_API_KEY`

## Automation (via Make.com)

Connect Notion to other tools:
- Paystack → Notion (new payments)
- Gmail → Notion (important emails)
- GitHub Issues → Notion (sync updates)

## Links

- [Notion Workspace](https://www.notion.so)
- [Notion API Docs](https://developers.notion.com/)
- [Database Templates](https://www.notion.so/templates)
