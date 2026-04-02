# Official Grain MCP Server: Quick Start Guide

The Grain MCP (Model Context Protocol) connects [Claude.ai](http://Claude.ai) (and [other](https://modelcontextprotocol.io/clients) AI chat clients) directly to your meeting data in Grain, enabling powerful [AI-powered individual workflows](#basic-usage-examples) as well as [customer and team analytics/reporting](#structured-reporting-examples) directly within Claude.ai. While we are working on support for ChatGPT (email [mike (at) grain (dot) com] if you want to be on the ChatGPT early access list), we encourage users who plan to prioritize MCP in their workflow to use Claude as it's support for MCP is currently meaningfully more mature and robust.

---

# Claude 60-Second Setup

**Getting Started Video:**

In this video I walk through the set-up steps that are also documented below. 

*Please note that if you're using the Teams or Enterprise versions there is a slight modification of the "Add Integration" step detailed in the first section below.*

[GSD_v1.mp4](https://media.grain.com/public/developer-docs/GSD_v1.mp4)

## Claude Paid Users

*Grain MCP supports easy setup as a native [Claude Integration](https://www.anthropic.com/news/integrations).*  

**Step 1: Integration Setup**

1. Navigate to **Settings** → **Integrations (Pro/Max Users)** → **Organization Settings (Team/Enterprise Users)**

![Screenshot 2025-06-16 at 3.14.59 PM.png](https://media.grain.com/public/developer-docs/Screenshot_2025-06-16_at_3.14.59_PM.png)

1. Click **"+ Add Integration"**

![Screenshot 2025-06-16 at 3.14.00 PM.png](https://media.grain.com/public/developer-docs/Screenshot_2025-06-16_at_3.14.00_PM.png)

1. Enter details and click the "**Add**" button:
- Integration Name: **Grain**
- Integration URL: **https://api.grain.com/_/mcp**

![Screenshot 2025-06-16 at 3.12.05 PM.png](https://media.grain.com/public/developer-docs/Screenshot_2025-06-16_at_3.12.05_PM.png)

**Step 2: Connection / Authentication**

From **Settings** → **Integrations:**

1. Look for "Grain" in the list of integrations and click "Connect"

![Screenshot 2025-06-16 at 2.55.12 PM.png](https://media.grain.com/public/developer-docs/Screenshot_2025-06-16_at_2.55.12_PM.png)

1. Once automatically redirected to Grain, click "**Approve**"

![Screenshot 2025-06-16 at 2.46.17 PM.png](https://media.grain.com/public/developer-docs/Screenshot_2025-06-16_at_2.46.17_PM.png)

**Step 3: Testing MCP Tools**

From a New Claude chat:

1. Click "Search and Tools" and confirm you can see "Grain" in the list

![Screenshot 2025-06-16 at 2.56.06 PM.png](https://media.grain.com/public/developer-docs/Screenshot_2025-06-16_at_2.56.06_PM.png)

1. Click "Grain" to confirm the MCP tools are active, toggle tools on/off as desired

![Screenshot 2025-06-16 at 2.57.26 PM.png](https://media.grain.com/public/developer-docs/Screenshot_2025-06-16_at_2.57.26_PM.png)

1. Test Connection by typing `"Tell me about my most recent Grain meeting"` or any other test prompt and Submit the chat

![Screenshot 2025-06-16 at 3.01.33 PM.png](https://media.grain.com/public/developer-docs/Screenshot_2025-06-16_at_3.01.33_PM.png)

If everything is set up properly, you'll see Claude make requests to the available Grain tools that are needed to fulfill the data needs of the Chat request. For best results, turn off non-Grain tools that may distract or confuse the LLM or cite the name and filters of the Grain tool you want it to use from the [Available MCP Tools](#available-mcp-tools) section.

## Claude Free Users & Other Clients (Developers Only)

<aside>
🚧

Please note that [`mcp-remote`](https://github.com/geelen/mcp-remote) is soon to be deprecated in favor of native client integrations and as such is not an officially supported method of connection by the official Grain MCP Server. Please plan your use of this connection method accordingly.

</aside>

**Cursor**

Click [Here](https://www.cursor.com/install-mcp?name=Grain&config=eyJ1cmwiOiJodHRwczovL2FwaS5ncmFpbi5jb20vXy9tY3AifQ%3D%3D) to Install

**Manual Configuration (All Other [Clients](https://modelcontextprotocol.io/clients))**

Prerequisites:

- Node.js installed ([nodejs.org](https://nodejs.org/))
- Claude Desktop App

**Verify Node.js Installation:**

Open terminal/command prompt and run:

```
node --version
```

If you get an error, install Node.js from [nodejs.org](https://nodejs.org/).

**Setup Steps:**

1. **Edit Config File**
    - **Settings** → **Developer** → **Edit Config**
    - Opens `claude_desktop_config.json`
2. **Add Configuration**
    
    ```json
    {
      "mcpServers": {
        "grain": {
          "command": "npx",
          "args": ["-y", "mcp-remote", "https://api.grain.com/_/mcp"]
        }
      }
    }
    ```
    
3. **Restart Application**
    - Close and reopen Claude Desktop
    - Verify "Grain" appears in **Settings** → **Integrations**
4. **Enable Tools**
    - Select **Tools and Settings** for Grain
    - Verify all tools are enabled
    - Allow tools when prompted in conversations

**Test Connection:**

```
List my recent Grain meetings
```

# ChatGPT Quick Setup

<aside>
🗒️

NOTE: Connectors are only available in ChatGPT for Pro accounts at [chat.openai.com](https://chat.openai.com/), and specifically in:

- Web interface (desktop browser)
- Latest native desktop apps (Mac/Windows)

They are not available in:

- Mobile apps (Connectors are limited there)
- Third-party integrations (like Slack, plugins, or API use)
- ChatGPT for Teams or Enterprise accounts may have admin restrictions disabling connectors.

**UPDATED NOTE:** 

- Though OpenAI's documentation states that connectors set up by an admin should be accessible by the whole team, we have found that the connector only works for the admin who set up the connector. This is a limitation on OpenAI's side, and effects all custom connectors. See [OpenAI's developer community](https://community.openai.com/t/custom-mcp-connector-only-works-for-person-who-set-it-up/1335021/8) for more information.
- To get the connector to work, you will have to enable the connection before beginning a conversation. You cannot set up the connector mid-conversation. This is also a limitation of OpenAI.
</aside>

1. Go to [**chat.openai.com](https://chat.openai.com/)** and sign into your ChatGPT Pro account

![Grain0.png](https://media.grain.com/public/developer-docs/Grain0.png)

1. Go to settings and navigate to "Connectors" 

![Grain1.png](https://media.grain.com/public/developer-docs/Grain1.png)

1. Set up Grain as a connector using the url [https://api.grain.com/_/mcp](https://api.grain.com/_/mcp)

![Grain2.png](https://media.grain.com/public/developer-docs/Grain2.png)

1. Grant ChatGPT access to your Grain Account data

![Grain3.png](https://media.grain.com/public/developer-docs/Grain3.png)

![Grain5.png](https://media.grain.com/public/developer-docs/Grain5.png)

1. Enable Grain as a source and begin your work! 

*Note: you will need to open a new chat and enable Grain as a connector before beginning each query. If you have already started a chat, Grain will be greyed out as a connector option.*

![Grain4.png](https://media.grain.com/public/developer-docs/Grain4.png)

---

# Available MCP Tools

### Free & Starter Plan MCP Tools

- **`myself`** : Get your Grain account information
    
    **Parameters**: None
    
- **`list_meetings / list_attended_meetings`:** Get filtered list of all accessible meetings
    
    **Key Parameters**:
    
    - `filters` (optional): Object containing:
        - `companies`: Array of company IDs (use `search_companies` first)
        - `persons`: Array of person IDs (use `search_persons` first)
        - `after_datetime`: ISO 8601 formatted datetime (e.g., "2024-01-01T00:00:00Z")
        - `before_datetime`: ISO 8601 formatted datetime
        - `participant_scope`: "internal" | "external"
        - `title_search`: Substring to match in meeting titles
    - `limit`: Results per page (1-20, default 10)
    - `cursor`: For pagination
- **`fetch_meeting`:** Get detailed information about a specific meeting
    
    **Key Parameters**:
    
    - `meeting_id`: UUID of the meeting
- **`fetch_meeting_transcript`**: Retrieve full meeting transcript
    
    **Key Parameters**:
    
    - `meeting_id`: UUID of the meeting
    - `include_timestamps`: Boolean (default: false)
- **`fetch_meeting_notes`:** Get AI-generated meeting notes (more concise than transcripts)
    
    **Parameters**:
    
    - `meeting_id`: UUID of the meeting
- **`search_meetings`:** Semantic search across all meeting transcripts
    
    **Key Parameters**:
    
    - `search_string`: Your search query (longer strings = more focused results)
    - `filters`: Same meeting filters as `list_meetings`
    - `limit`: Results to return (1-50, default 10)
    - `speaker_scope`: "all" | "internal" | "external" (default: all)
- **`search_companies`:** Find companies that participated in meetings when filtering
    
    **Key Parameters**:
    
    - `search_string`: Company name or domain
    - `filters`: Standard meeting filters
    - `limit`: Results to return (1-20, default 10)
- **`search_persons`** : Search for meeting participants when filtering
    - `search_string`: Person's name or email
    - `filters`: Standard meeting filters
    - `limit`: Results to return (1-20, default 10)
- **`list_workspace_users`** : Get all users in your Grain workspace
    
    **Parameters**: None
    

### Business & Enterprise Plan MCP Tools

- **`list_coaching_feedback`** : Get AI-generated sales coaching insights
    
    **Key Parameters**:
    
    - `filters.has_coaching_opportunities`: Set to `true` for flagged opportunities only
    - Standard meeting filters apply
- **`fetch_meeting_coaching_feedback` :** Get detailed coaching scorecard for specific meeting
    
    **Parameters**:
    
    - `meeting_id`: UUID of the meeting
- **`list_open_deals` / `list_all_deals` :** Access HubSpot Deal intelligence
    
    **Key Parameters**:
    
    - `filters` (optional): Object containing:
        - `companies`: Array of company IDs (UUIDs)
        - `deal_at_risk`: Boolean to filter at-risk deals
        - `deal_owner`: Person ID (UUID) of deal owner
        - `pipeline`: HubSpot pipeline ID
        - `title_search`: Substring to match in deal titles
    - `limit` (optional): Results per page (1-20, default 10)
    - `cursor` (optional): For pagination
- **`fetch_deal`** : Get detailed deal information
    
    **Parameters**:
    
    - `deal_id`: UUID of the deal

---

# Basic Usage Examples

Start with these foundational prompts to explore your meeting data.

**Getting Started (First Steps)**

- `Show me all action items I'm responsible for from the past 7 days`
- `Help me draft all follow-up emails for my external meetings today`

**Customer Intelligence**

- `Summarize customer mentions of pricing concerns in the last 30 days`
- `Help me understand how customers are comparing us with competitors`

**People & Company Insights**

- `Who from {Company Name} have we met with and what topics did we cover?`
- `Show me all users who mentioned feature requests or product feedback recently`

**Deal & Business Analysis**

- `What objections came up in external sales calls this week?`
- `Show me deals that haven't had meetings in the last 2 weeks`

**Content Discovery**

- `Search for discussions about our new product features`
- `What were the key decisions made in this week's internal meetings?`

---

# Structured Reporting Examples

**Using MCP Prompts**

While MCP Tools are designed to work with any natural language inputs into Chat, [Prompts](https://modelcontextprotocol.io/docs/concepts/prompts) are manually selected/triggered by the user to chain multiple tool calls together in a structured and repeatable way. The result is a set of comprehensive analysis workflows that would take hours manually but complete in minutes. We have created a initial library of 9 officially supported Prompts accessible directly within Claude.ai, you can riff on our templates to create your own prompts by copy/pasting your own changes to the prompt's instructions.

**How to Use:**

1. **Click the + Button** in the bottom left of the Claude chat window
2. **Click "Add from Grain"** in the options list and choose a report to run
3. **Submit Prompt to Claude** with any (optional) custom instructions in the chat window
4. **Input Variables** when prompted by Claude as needed

![Screenshot 2025-06-16 at 5.25.10 PM.png](https://media.grain.com/public/developer-docs/Screenshot_2025-06-16_at_5.25.10_PM.png)

---

## Product & Market Intelligence

*Broad market insights and specific feature/competitive deep-dives*

### Voice of Customer Insights Report

**Prompt Name**: `voice_of_customer_insights_report`

**Use for**: Product roadmap priorities, market trends, customer satisfaction

**Arguments**:

- `analysis_days` (optional): Days of customer feedback to analyze (default: 120)

**Implementation**:

This prompt uses the following Grain MCP tools in sequence:

1. `list_meetings` - Get external meetings with customers
2. `search_meetings` - Find pain points, feature requests, and success stories
3. `search_companies` - Segment feedback by customer type
4. `fetch_meeting_notes` - Extract detailed insights and quotes

*Copy/Paste the below into any AI Chat Client w/ Grain MCP active or use Prompts in Claude.ai*

```markdown
Extract customer insights across all feedback channels over the last {analysis_days*} days:

Step 1: Comprehensive data collection
- Use list_meetings* with participant_scope=external to find external meetings with customer pain points mentioned
- Use search_meetings *to find feature requests and enhancement discussions
- Use search_meetings* to identify implementation challenges and successes
- Use search_meetings *to locate competitive comparisons and concerns

Step 2: Pain point categorization:
- Use search_meetings* to categorize product functionality gaps
- Use search_meetings *to identify integration limitations
- Use search_meetings* to find user experience friction
- Use search_meetings *to document performance or reliability issues
- Use search_meetings* to extract pricing and value concerns

Step 3: Success story identification:
- Use search_meetings *to find positive outcome testimonials
- Use fetch_meeting_notes to extract ROI and value realization examples
- Use search_meetings* to document workflow improvements achieved
- Use search_meetings *to identify team adoption successes

Step 4: Feature demand analysis:
- Analyze request frequency by feature category
- Use search_companies* to identify customer segment patterns
- Assess business impact and urgency levels
- Evaluate technical complexity vs. customer value

Step 5: Actionable insights:
- Generate product roadmap priorities with customer backing
- Identify customer success best practices
- Recommend support process improvements
- Highlight competitive positioning opportunities

Include specific customer quotes and quantified impact data.
```

*Example of reporting output from the prompt (redacted and shortened)*

<aside>
📣

[Redacted Example] **Voice of Customer Insights Report - Q2**

*This report represents comprehensive analysis of voice of customer feedback and should be used to inform product roadmap, marketing strategy, and customer success initiatives.*

**Executive Summary**

Based on analysis of **## external customer meetings** over the last ## days, our platform is positioned strongly as a cost-effective alternative to enterprise solutions like Competitor A, with customers consistently recognizing ##-##% feature parity at a fraction of the cost. The analysis reveals clear patterns in customer segments, pain points, and success factors that should inform product roadmap and go-to-market strategy.

---

**Supporting Data Sourcescl**

**Meeting Analysis:** ## external customer meetings
**Customer Segments:** ##+ companies across ##+ industries
**Feature Requests:** ##+ specific enhancement requests catalogued
**Competitive Intelligence:** Direct feedback from ##+ Competitor A migration prospects

**Key Findings:**

- **##% of our ##+ customers** are in financial services
- **Primary competitive advantage:** #-##x cost savings vs. Competitor A with comparable functionality
- **Top customer segments:** SMB/Mid-market sales teams, financial advisors, recruiting agencies
- **Biggest opportunity:** "Feature X" consistently requested across customer base

---

**Customer Segment Analysis**

**Primary Segments**

**1. SMB/Mid-Market Sales Teams (##% of conversations)**

- **Size:** #-## employees
- **Pain:** Competitor A too expensive ($##+ for # users), long contracts, seat minimums
- **Value Prop:** Same features, 1/#th the cost, month-to-month flexibility
- **Examples:** Company A (tech vertical), Company B (software), Company C (payments)

**2. Financial Services (##% of customer base)**

- …. [example reduced for length]

… [example reduced for length]

</aside>

---

## Deal Intelligence

*Big picture view of all deals and individual deal deep-dives.*

**[All reports require Grain Business or Enterprise account with an active HubSpot Integration]**

### Deal Pipeline Intelligence Report

**Prompt Name**: `deal_pipeline_intelligence_report`

**Use for**: Portfolio overview, resource allocation, trend analysis

**Arguments**:

- `days_back` (required): Number of days to analyze (default: 60)
- `risk_threshold` (optional): Deal age threshold for high risk classification (default: 15)

**Implementation**:

This prompt uses the following Grain MCP tools in sequence:

1. `list_open_deals` - Get all active deals
2. `list_meetings` - Find meetings for each deal
3. `fetch_meeting_notes` - Analyze discussion content
4. `search_meetings` - Find competitive mentions and objections

```markdown
*Analyze active deal health and progression over the last {days_back} days:

Step 1: Get all open deals with recent activity
- Use list_open_deals to retrieve active opportunities
- Include deal metadata: stage, momentum, risk status, scores

Step 2: For each deal with external meetings:
- Use fetch_deal filtered by company to get meeting history
- Analyze deal age and progression velocity
- Review stakeholder engagement patterns
- Assess meeting frequency trends vs. stage requirements
- Use fetch_meeting_notes to extract key discussion topics and pain points
- Use search_meetings for competitive mentions and objections
- Evaluate next steps clarity and follow-through

Step 3: Risk assessment by category:
- HIGH RISK: Stalled momentum, {riskthreshold}+ days old, low scores
- MEDIUM RISK: Slowing momentum, integration concerns
- HEALTHY: Progressing momentum, recent activity, clear next steps

Step 4: Generate actionable recommendations:
- Immediate interventions for at-risk deals
- Expansion opportunities in healthy accounts
- Specific next steps with timelines
- Resource allocation priorities

Include deal IDs, company names, and specific quotes from meetings.*
```

<aside>
🏗️

[Redacted Example] **Deal Pipeline Intelligence Report - Last 30 Days**

---

**Executive Summary**

**Pipeline Health Score: 6.5/10**

Our active deal pipeline shows mixed signals with **[X] open deals** across various stages, but concerning patterns emerge around deal momentum and progression velocity. While most deals show positive initial engagement (average call score: 3.5/5), **[X]% are flagged as at-risk** with stalled or slowing momentum.

**Key Concerns:**

- [X] deals marked as "at-risk" with stalled momentum
- Multiple deals stuck in "Demo Set" stage beyond optimal timeframes

**Positive Indicators:**

- Strong initial call scores (3-4/5) indicating good product-market fit
- Recent demos showing high engagement (Company B: 4/5 score)

*Report generated from sales platform data covering [DATE RANGE REDACTED]Next review: [DATE REDACTED]*

---

**Deal Segmentation Analysis**

🔴 HIGH RISK DEALS ([X] deals)

*Immediate intervention required - 15+ days old, stalled momentum*

| Company | Deal ID | Age | Status | Next Action Required |
| --- | --- | --- | --- | --- |
| **Company C** | [REDACTED] | [X] days | Slowing | Follow-up on competitor comparison decision |
| **Company D** | [REDACTED] | [X] days | Stalled | Reschedule technical demo |
| **Company E** | [REDACTED] | [X] days | Stalled | Enterprise security review follow-up |

🟡 MEDIUM RISK DEALS ([X] deals)

*Monitoring required - showing momentum concerns*

| Company | Deal ID | Age | Status | Key Issue |
| --- | --- | --- | --- | --- |
| **Company I** | [REDACTED] | [X] days | Slowing | CRM integration requirements |
| **Company J** | [REDACTED] | [X] days | Slowing | No recent activity |
| **Company K** | [REDACTED] | [X] days | Slowing | Post-demo follow-up needed |

🟢 HEALTHY DEALS ([X] deals)

*Progressing momentum, active engagement*

| Company | Deal ID | Age | Status | Strength Indicators |
| --- | --- | --- | --- | --- |
| **Company A** | [REDACTED] | [X] days | **IN TRIAL** | $[X]K opportunity, active usage |
| **Company B** | [REDACTED] | [X] days | Progressing | High engagement, API requirements |

---

**Common Success Patterns**

🎯 **What's Working Well**

1. **Strong Initial Demos**: Average call score of 3.5/5 indicates good product-market fit
2. **API-First Customers**: Companies with specific API requirements (X, Y) show stronger progression
3. **CRM Integration Alignment**: Deals with HubSpot/Salesforce show better momentum
4. … [example reduced for length]

…[example reduced for length]

---

</aside>

### Health Report By Deal

**Prompt Name**: `health_report_by_deal`

**Use for**: Specific deal strategy, stakeholder mapping, next step planning

**Arguments**:

- `deal_name` (required): Deal name or company name to analyze
- `analysis_days` (optional): Days of meeting history to analyze (default: 90)

**Implementation**:

This prompt uses the following Grain MCP tools in sequence:

1. `search_companies` - Find company ID by name
2. `fetch_deal` - Get deal metadata if available
3. `list_meetings` - Get all meetings with the company
4. `fetch_meeting_notes` - Extract key insights from each meeting
5. `search_meetings` - Find specific topics like competitors or objections

```markdown
Analyze the health and momentum of {deal*name}:

Step 1: Deal identification and context
- Use search_companies* to find company ID for "{deal*name}"
- Use fetch*deal to retrieve deal metadata: stage, age, owner, risk status, scores
- Use search*persons to identify key stakeholders and contacts involved

Step 2: Meeting Analysis Sources table
Create a reverse chronological table with:
- Date, Meeting Title, Duration
- Attendees (exclude bot/notetaker names)
- Upshot: 15-word-or-less summary of purpose and outcome
- Source: Percentage indicating relative importance to analysis

Step 3: Meeting activity analysis
- Use fetch_deal* filtered by company to find all associated meetings
- Analyze meeting frequency and timing patterns over last {analysis_days*} days
- Review participant engagement and attendance
- Track progression through sales stages

Step 4: Content analysis of conversations
- Use fetch_meeting_notes to extract key discussion topics and pain points
- Use search_meetings* to identify decision criteria and evaluation process
- Use search_meetings for competitive mentions and objections
- Note buying signals and momentum indicators

Step 5: Stakeholder mapping and engagement
- Map decision makers, influencers, and champions from meeting attendees
- Analyze engagement levels of key participants
- Identify missing stakeholders or access gaps
- Review multi-threading effectiveness

Step 6: Risk assessment and recommendations
- Evaluate deal progression velocity vs. stage requirements
- Identify stall indicators or momentum shifts
- Assess competitive threats and positioning
- Generate specific next steps with timelines

Include deal score trends, specific quotes, and actionable recommendations.
```

<aside>
📣

**[Redacted Example] Deal Health Analysis Report**

**Executive Summary**

**Overall Health: MODERATE RISK**
The prospect shows strong product-market fit and buyer intent, but faces execution challenges and potential timeline risks due to missing critical feature requirements.

**Key Metrics:**

- Deal Value: [REDACTED]
- Stage: Customer In Trial
- Deal Age: [X] days (opened [DATE])
- Momentum: Progressing (not at risk)
- Owner: [SALES REP NAME]

---

**Deal Context**

**Company:** [COMPANY NAME] - AI-based business communication platform
**Key Contact:** [PRIMARY CONTACT] ([EMAIL])
**Current State:** In trial with [X] users added
**Competing Solution:** Currently using [COMPETITOR] ([X] users for [X]+ years)

---

**Meeting Activity Overview**

| Date | Meeting | Duration | Attendees | Upshot | Source |
| --- | --- | --- | --- | --- | --- |
| [DATE] | Product Demo | [X]:[X] | [PRIMARY CONTACT], [SALES REP] | Product feedback session; trial requested | Primary |

**Critical Note:** Only one recorded meeting - limited engagement data for comprehensive analysis.

**Timeline Overview:**

- **[DATE]:** Welcome trial email sent
- **[DATE]:** Follow-up email about team collaboration
- **[DATE]:** Demo call conducted
- **Current:** Deal moved to "Customer In Trial" stage

**Engagement Patterns:**

- **Positive:** Quick progression from trial start to demo ([X] days)
- **Concerning:** Only one meeting in [X]-day deal cycle
- **Neutral:** Customer initiated trial independently and added team members

---

## Conversation Analysis

Pain Points Identified:

1. **Current Tool Limitations:** [COMPETITOR] works but lacks conversational intelligence
2. **Missing Features:** No coaching/empowerment capabilities in current solution
3. … [example reduced for length]

…[example reduced for length]

</aside>

### SPICED Opportunity Matrix By Deal

**Prompt Name**: `spiced_opportunity_matrix_by_deal`

**Use for**: Comprehensive deal qualification, stakeholder alignment, forecasting accuracy

**Arguments**:

- `deal_name` (required): Deal name or company name to analyze
- `analysis_period` (optional): Days of meeting history to analyze (default: 180)

**Implementation**:

This prompt uses the following Grain MCP tools in sequence:

1. `search_companies` - Find company by name
2. `fetch_deal` - Get deal metadata and scores
3. `list_meetings` - Get comprehensive meeting history
4. `fetch_meeting_transcript` - Deep content analysis for SPICED elements
5. `search_meetings` - Find specific SPICED criteria discussions

```markdown
Generate a complete SPICED analysis for {deal*name}:

Step 1: Deal identification and meeting collection
- Use search_companies* to find company ID for "{deal*name}"
- Use list_open_deals and fetch_deal to get deal metadata if available
- Use fetch*deal to get deal metadata if available
- Use list_meetings *to find all meetings with this company over {analysis_period*} days
- List participants and their roles across all meetings
- Create timeline of interactions and progression

Step 2: Meeting Analysis Sources table
Create a reverse chronological table with:
- Date, Meeting Title, Duration
- Attendees (exclude bot/notetaker names)
- Upshot: 15-word-or-less summary of purpose and outcome
- Source: Percentage indicating relative importance to SPICED analysis

Step 3: SITUATION analysis from meeting content
Use fetch*meeting*transcript to extract and document background facts:
- Company size, locations, and organizational structure mentioned
- Current technology stack and existing solutions
- Recent initiatives, changes, or strategic shifts discussed
- Industry context and market position
- Key business metrics or KPIs referenced

Step 4: PAIN identification and prioritization
Use search_meetings *to analyze all meetings for pain points:
- Quantifiable pains: Measurable business challenges with metrics
- Qualitative pains: Emotional or subjective challenges expressed
- Pain evolution: How pains have changed/evolved across meetings
- Pain prioritization: Which pains are mentioned most frequently
- Direct quotes expressing frustration or challenges

Step 5: IMPACT assessment and business case
Use fetch*meeting_notes to document desired outcomes and value:
- Revenue increase opportunities mentioned
- Cost reduction possibilities discussed
- Customer experience improvements sought
- Individual/emotional impacts for stakeholders
- ROI discussions and value quantification attempts
- Success metrics and KPIs they want to achieve

Step 6: CRITICAL EVENT timeline and urgency
Identify all timing drivers:
- Hard deadlines mentioned (board meetings, renewals, launches)
- Compelling events creating urgency (hiring, compliance, competition)
- Consequences of missing deadlines explicitly discussed
- Timeline evolution: How dates have shifted across meetings
- Test questions asked about timing importance

Step 7: DECISION process mapping
Comprehensive decision analysis:
- Decision process: Steps and stages they've outlined
- Decision committee: All stakeholders mentioned and their roles
  - Economic buyer identification
  - Technical evaluators
  - Executive sponsors
  - Influencers and blockers
- Decision criteria: Evaluation factors discussed
  - Technical requirements
  - Integration needs
  - Budget constraints
  - Security/compliance requirements
- Previous purchase experiences mentioned
- Procurement/legal requirements identified

Step 8: Competitive landscape and status quo
- Current solution pain points and limitations
- Competitors being evaluated (direct mentions)
- Evaluation criteria comparisons
- Differentiation points discussed
- Risk of no decision vs. competitive loss

Step 9: SPICED opportunity matrix generation
Create a structured summary table:
- Situation: 3-5 key facts
- Pain: Top 3 quantifiable and qualitative pains
- Impact: Primary business impacts with metrics
- Critical Event: Specific date and consequences
- Decision: Process flowchart and committee map

Step 10: Deal qualification and forecast accuracy
- SPICED completeness score (what's known vs. unknown)
- Strength of pain/impact connection
- Critical event credibility assessment
- Decision process clarity and access
- Overall deal qualification rating
- Recommended discovery gaps to fill

Step 11: Strategic recommendations
- Next discovery questions to ask
- Stakeholders to engage based on SPICED gaps
- Value proposition alignment with impacts
- Timeline acceleration opportunities
- Risk mitigation strategies

Include specific quotes for each SPICED element, meeting references, and a visual opportunity matrix summary.
```

<aside>
🌶️

[Redacted Example] **SPICED Opportunity Matrix: COMPANY NAME (SUBSIDIARY NAME)**

**Deal Overview:**

- **Deal Name:** [COMPANY NAME] (previously [SUBSIDIARY NAME])
- **Deal Value:** $[AMOUNT]
- **Deal Owner:** [SALES REP NAME]
- **Stage:** Customer In Trial
- **Status:** AT RISK - Stalled momentum (Latest call score: [SCORE])
- **Pipeline:** New Business
- **Opened:** [DATE]

**Key Participants Timeline:**

- **[NAME 1]** - Senior Manager, Spatial -omics ([EMAIL]) - Champion
- **[NAME 2]** - Director, IT Infrastructure ([EMAIL]) - Technical Evaluator
- **[NAME 3]** - CEO (mentioned but not directly engaged)
- **[NAME 4]** - VP of Sales (mentioned as decision influencer)

---

**Meeting Analysis Sources**

| Date | Meeting Title | Duration | Attendees | Upshot | Source % |
| --- | --- | --- | --- | --- | --- |
| [DATE] | [COMPANY] <> Grain Trial Recap | [TIME] | [NAME 2], [SALES REP] | User feedback collection underway, decision pending | [X%] |
| [DATE] | [NAME 1] and [GRAIN EMPLOYEE] | [TIME] | [NAME 1], [GRAIN EMPLOYEE] | Security settings bug escalated to engineering | [Y%] |
| [DATE] | [NAME 2] and [GRAIN EMPLOYEE] | [TIME] | [NAME 2], [GRAIN EMPLOYEE] | Product demo, pilot program setup, competitive evaluation | [Z%] |

**SPICED Opportunity Matrix Summary**

| Element | Status | Key Facts |
| --- | --- | --- |
| **SITUATION** | ✅ Well-Qualified | Post-acquisition, [NUMBER] employees, [NUMBER] seat target, distributed sales team |
| **PAIN** | ⚠️ Moderate | Manual processes, speaker ID issues, security concerns, geographic challenges |
| **IMPACT** | ⚠️ Moderate | Sales coaching scale, process efficiency, $[AMOUNT] deal value identified |
| **CRITICAL EVENT** | 🔴 Urgent | CEO-driven initiative, [TIMEFRAME] decision timeline, competitive evaluation |
| **DECISION** | ⚠️ Moderate | Clear committee identified, champion in place, process defined but conservative culture |

**SITUATION Analysis**

**Company Structure & Size:**

- Post-acquisition organization: [PARENT COMPANY] acquired [SUBSIDIARY NAME]
- ~[NUMBER] total employees at [PARENT COMPANY]
- Target user base: [NUMBER] seats (minimum [NUMBER] sales reps + managers, plus R&D teams)
- Geographic spread: Sales team across the whole country

**Technology Environment:**

- Outdated technology practices: "They live in [YEAR]" - manual Excel sheets, time cards
- Legacy Salesforce usage: Manual note transcription and activity logging
- Current evaluation: Comparing Grain vs. [COMPETITOR 1] vs. [COMPETITOR 2] vs. [COMPETITOR 3]

**Organizational Context:**

- Conservative management culture: [NUMBER]+ year tenured leadership (CEO [NAME 3], VP Marketing [NAME 5])
- Recent acquisition integration challenges
- Champion ([NAME 1]) facing internal resistance but gaining traction

**Current Grain Usage:**

- [NUMBER] active members in [SUBSIDIARY] workspace
- [NUMBER]+ years of historical data and recordings

---

**PAIN Identification and Prioritization**

Quantifiable Pains:

1. **Manual Note-Taking Inefficiency:** Sales reps manually transcribing meeting notes into Salesforce
    - *Quote:* "They're taking notes and they have to transcribe it. Then they have to put the meeting notes on the person under an activity. It's just stupid." - [NAME 1]
2. **Speaker Identification in Conference Rooms:** Cannot identify individual speakers in group meetings
    - *Quote:* "Who's talking? Who are all people sitting in the same conference room showing up as just like [NAME 3]" - [NAME 2]
3. … [example reduced for length]

…[example reduced for length]

</aside>

### MEDDICC Diagnosis Report By Deal

**Prompt Name**: `meddicc_diagnosis_report_by_deal`

**Use for**: Enterprise deal qualification, complex sales cycles, multi-stakeholder opportunities

**Arguments**:

- `deal_name` (required): Deal name or company name to analyze
- `analysis_period` (optional): Days of meeting history to analyze (default: 180)

**Implementation**:

This prompt uses the following Grain MCP tools in sequence:

1. `search_companies` - Find company by name
2. `fetch_deal` - Get deal metadata and qualification scores
3. `list_meetings` - Get comprehensive meeting history
4. `fetch_meeting_transcript` - Deep content analysis for MEDDICC elements
5. `search_meetings` - Find specific qualification criteria
6. `search_persons` - Map stakeholders and decision makers

```markdown
Generate a complete MEDDICC analysis for {deal*name}:

Step 1: Deal identification and meeting collection
- Use search_companies* to find company ID for "{deal*name}"
- Use list_open_deals and fetch_deal to get deal metadata if available*
- Use list_meetings *to find all meetings with this company over {analysis_period*} days
- Use search_persons to list participants and their roles across all meetings
- Create timeline of interactions and progression

Step 2: Meeting Analysis Sources table
Create a reverse chronological table with:
- Date, Meeting Title, Duration
- Attendees (exclude bot/notetaker names)
- Upshot: 15-word-or-less summary of purpose and outcome
- Source: Percentage indicating relative importance to MEDDICC analysis

Step 3: METRICS identification and quantification
Extract measurable success criteria:
- Specific KPIs and targets mentioned
- Current performance baselines discussed
- Improvement goals with numbers and timelines
- ROI expectations and calculations shared
- Success measurement criteria defined

Step 4: ECONOMIC BUYER mapping
Identify and analyze the economic buyer:
- Name, title, and direct influence confirmed
- Budget authority validation
- Meeting participation and engagement level
- Direct quotes showing financial decision power
- Access level achieved and relationship strength

Step 5: DECISION CRITERIA documentation
Catalog all evaluation criteria mentioned:
- Technical requirements and specifications
- Business/operational requirements
- Financial constraints and budget parameters
- Timeline and implementation needs
- Competitive evaluation criteria
- Weighting or priority of criteria

Step 6: DECISION PROCESS analysis
Map the complete buying process:
- Formal steps outlined by customer
- Informal political dynamics observed
- Approval stages and sign-offs required
- Committee members and voting process
- Timeline for each stage
- Current stage and next steps

Step 7: IDENTIFY PAIN deep dive
Comprehensive pain analysis:
- Business pains with quantified impact
- Technical pains affecting operations
- Personal pains for key stakeholders
- Pain severity and urgency ratings
- Consequences of inaction discussed
- Pain ownership and accountability

Step 8: CHAMPION qualification
Assess champion strength and capability:
- Name and role of potential champions
- Evidence of internal selling activities
- Power and influence demonstrated
- Personal win if project succeeds
- Ability and willingness to provide intel
- Risk if champion is removed/changes

Step 9: COMPETITION assessment
Analyze competitive landscape:
- Direct competitors being evaluated
- Incumbent solution strengths/weaknesses
- Competitive advantages articulated
- Vulnerabilities and differentiation points
- Decision criteria favoring us vs. them
- Competitive strategy and positioning

Step 10: MEDDICC scoring and gaps
Create qualification scorecard:
- Score each MEDDICC element (1-5)
- Identify missing information per element
- Risk assessment for weak areas
- Strength indicators for leverage
- Overall deal qualification score

Step 11: Strategic action plan
Based on MEDDICC analysis:
- Critical gaps requiring immediate discovery
- Stakeholder engagement priorities
- Champion development strategies
- Competitive positioning tactics
- Risk mitigation approaches
- Specific next steps with owners and dates

Include quantified metrics, specific quotes, and a MEDDICC scorecard summary.
```

<aside>
Ⓜ️

[Redacted Example] MEDDICC Analysis: [COMPANY A] (Previously [COMPANY B])

**Deal Overview:** $[XXX] ARR | Customer In Trial | At Risk - Stalled

---

**Deal Identification and Meeting Collection**

**Company:** [COMPANY A] (previously [COMPANY B])

**Deal ID:** [REDACTED]

**Deal Owner:** [SALES REP A]

**Pipeline:** New Business

**Current Stage:** Customer In Trial

**Deal Status:** At Risk - Stalled

**Timeline:** Acquisition occurred [MONTH YEAR], deal opened [DATE], closed [DATE], currently in trial.

---

**Meeting Analysis Sources Table**

| Date | Meeting Title | Duration | Attendees | Upshot | Source |
| --- | --- | --- | --- | --- | --- |
| [DATE] | [COMPANY A] <> [VENDOR] Trial Recap | [TIME] | [SALES REP A], [CONTACT A] | User feedback collection underway, decision pending | [X]% |
| [DATE] | [CONTACT B] and [SUPPORT REP] | [TIME] | [SUPPORT REP], [CONTACT B] | Security settings troubleshooting, larger company evaluation concerns | [Y]% |
| [DATE] | [CONTACT A] and [SALES REP B] | [TIME] | [SALES REP B], [CONTACT A] | Product demo, pilot discussion, competitive evaluation setup | [Z]% |

---

**MEDDICC Scoring and Gaps**

**Overall MEDDICC Score: [X.X]/5 ([XX]%)**

| Element | Score (1-5) | Evidence | Gaps |
| --- | --- | --- | --- |
| **METRICS** | 4 | Clear expansion metrics ([XXX] users), efficiency gains quantified | ROI calculations not formalized |
| **ECONOMIC BUYER** | 2 | Identified ([EXECUTIVE A]) but no direct contact | Zero engagement with true decision maker |
| **DECISION CRITERIA** | 3 | Technical and business requirements understood | Formal criteria weighting unknown |
| **DECISION PROCESS** | 3 | Process steps identified, timeline established | Approval structure assumptions not validated |
| **IDENTIFY PAIN** | 4 | Multiple pain points quantified and urgent | CEO pain awareness uncertain |
| **CHAMPION** | 3 | Strong champion with good intel but limited access | Champion at risk, no executive-level champion |
| **COMPETITION** | 4 | Primary competitor identified, differentiation clear | Competitive decision criteria not confirmed |

---

**METRICS Identification and Quantification**

Current Performance Baselines

- **Usage Volume:** [COMPANY B] team had [X]+ years of meeting recordings stored
- **Team Size:** Currently [X]-[X] active users in workspace
- **Meeting Types:** Both internal calls and customer-facing sales calls
- **Geographic Scope:** Sales team "across the whole country"

Improvement Goals and Targets

- **Efficiency Gain:** [CONTACT B] noted impossible to "take notes and really pay attention to the customer at the same time"
- **Sales Coaching:** VP of Sales impressed by action items and commitments tracking vs. manual [TOOL] process
- **Foreign Customer Support:** AI handles "different accents" effectively for international customers

Expansion Metrics

- **Target User Base:** [XX]-[XXX] seats (confirmed by [CONTACT B])
    - "[XX] reps. Roughly [XX] reps and managers"
    - "they want to use it internally as well... R and D team"
    - "[XXX] people in the company... probably [XXX] people on the top end"

ROI Indicators

- **Time Savings:** Elimination of manual note transcription to [CRM SYSTEM]
- **Historical Data Value:** "It's super valuable" - risk of losing [X]+ years of recordings
- **Process Improvement:** From [SPREADSHEET TOOL] sheets and manual processes to automated AI summaries

---

**ECONOMIC BUYER Mapping**

Primary Economic Buyer

**Name:** [EXECUTIVE A]

**Title:** CEO

**Email:** [REDACTED]

**Authority Level:** Ultimate decision maker for [XX]-[XXX] seat deployment
**Budget Authority:** Confirmed - "the CEO is looking into AI Note takers"

**Engagement Status:** **NO DIRECT CONTACT ESTABLISHED**

Secondary Economic Buyer

… [example reduced for length]

</aside>

---

## Account & Customer Health

*Cross-account trends and individual account deep-dives*

### Recently Active Accounts Health Report

**Prompt Name**: `recently_active_accounts_health_report`

**Use for**: Portfolio triage, expansion opportunities, churn risk identification

**Arguments**:

- `analysis_days` (optional): Days to analyze meeting activity (default: 90)
- `account_count` (optional): Number of top accounts to analyze (default: 5)

**Implementation**:

This prompt uses the following Grain MCP tools in sequence:

1. `list_meetings` - Get meetings with external participants
2. `search_companies` - Identify most active companies
3. `fetch_meeting_notes` - Analyze sentiment and topics
4. `search_meetings` - Find risk indicators and concerns

```markdown
Analyze the health of my top {*account*_*count} accounts based on recent meeting activity:

1. Use list_meetings* with external participant filter to identify companies with the most meetings in the last {analysis_days*} days
2. For each company, use multiple tools to analyze:
   - Use list_meetings* to assess meeting frequency trends
   - Use *search*_*persons to review participant engagement levels
   - Use fetch_meeting_notes to extract key topics and concerns discussed
   - Use search_meetings* to track sentiment progression over time
   - Use search_meetings to identify risk indicators (missed meetings, unresolved issues)
3. Provide specific recommendations for each account
4. Flag any accounts that need immediate attention

Focus on companies where we've had external participants.
```

<aside>
🏥

[Redacted Example] **Top 5 Most Active Accounts (Last 30 Days)**

Based on meeting frequency, participant engagement, and strategic importance, here's the health analysis of your top 5 accounts:

---

🔴 **HIGH RISK - IMMEDIATE ATTENTION REQUIRED**

1. Company A - *CRITICAL CHURN RISK*

- **Meeting Frequency**: High (Multiple meetings in past X weeks)
- **Account Status**: 🚨 **PARTIAL CHURN IMMINENT**
- **Key Issues**:
    - Service delivery team actively looking at competitors
    - Access control and sharing problems causing operational friction
    - Missed deliverables due to sharing issues, frustrating team members
    - Currently testing alternative solutions

**Recent Activity Analysis**:

- [Date]: Critical escalation meeting about sharing groups
- [Date]: Key stakeholder meeting highlighting access frustrations

**Risk Indicators**:

- Quote: *"I think partial churn... service delivery is looking at other options because right now it's messy"*
- Quote: *"couple things were missed [recently] because of a sharing problem"*

**Immediate Actions Required**:

1. CEO-level engagement with service delivery team
2. Expedite "Teams" feature delivery (committed within X month)
3. Provide interim workaround solutions
4. Schedule weekly check-ins until resolution

---

🟡 **MEDIUM RISK - MONITOR CLOSELY**

2. Company B - *SCALING CHALLENGES*

- **Meeting Frequency**: Very High (XX meetings in XX days)
- **Account Status**: 🟡 **GROWING BUT COMPLEX**
- **Key Issues**:
    - Complex organizational structure requiring X+ workspaces
    - Privacy/compliance concerns for financial data
    - Training and adoption challenges across departments

**Recent Activity Analysis**:

- [Date]: Teams feature discussion for broader rollout
- Multiple coaching and presentation workshops throughout recent months

**Positive Indicators**:

- Committed to XX+ paid licenses
- … [example reduced for length]

… [example reduced for length]

</aside>

### Customer Health Report By Account

**Prompt Name**: `customer_health_report_by_account`

**Use for**: Account strategy, renewal planning, expansion tactics

**Arguments**:

- `account_name` (required): Company name to analyze
- `analysis_period` (optional): Days of history to analyze (default: 90)

**Implementation**:

This prompt uses the following Grain MCP tools in sequence:

1. `search_companies` - Find company by name and get contacts
2. `list_meetings` - Get comprehensive meeting history
3. `search_persons` - Map stakeholder relationships
4. `fetch_meeting_notes` - Analyze sentiment and topics
5. `search_meetings` - Track specific themes and concerns

```markdown
Comprehensive health analysis for {account_*name}:

Step 1: Account identification and baseline
- Use search_companies* to find company ID for "{account_*name}" and associated contacts
- Use list_meetings* to establish relationship timeline and tenure
- Identify account type (customer, prospect, partner) from meeting patterns
- Review account expansion history and potential from meeting progression

Step 2: Meeting Analysis Sources table
Create a reverse chronological table with:
- Date, Meeting Title, Duration
- Attendees (exclude bot/notetaker names)
- Upshot: 15-word-or-less summary of purpose and outcome
- Source: Percentage indicating relative importance to analysis

Step 3: Meeting engagement analysis ({analysis_period*}+ day period)
- Use list_meetings* to assess meeting frequency trends and consistency
- Use search_*persons to analyze stakeholder participation patterns
- Use fetch_*meeting_notes to review topic evolution and engagement depth
- Compare internal vs external meeting ratios

Step 4: Sentiment and satisfaction tracking
- Progression of sentiment over time
- Support issues and resolution patterns
- Feature requests and enhancement discussions
- Success stories and positive outcomes

Step 5: Business health indicators
- Usage growth or decline signals
- Team expansion or contraction mentions
- Budget and procurement discussions
- Renewal timeline and risk factors

Step 6: Relationship strength assessment
- Champion identification and engagement
- Executive access and relationship depth
- Cross-departmental usage and adoption
- Referral potential and advocacy signals

Step 7: Action plan and risk mitigation
- Immediate retention risks requiring intervention
- Expansion opportunities with specific tactics
- Relationship strengthening recommendations
- Timeline for next touchpoints and objectives

Focus on behavioral indicators, usage signals, and relationship quality metrics.
```

<aside>
🩺

[Redacted Example Output] **Comprehensive Customer Health Analysis - [COMPANY]**

**Account Status:** Strategic Partner & Customer

**Relationship Tenure:** [X]+ months

**Health Score:** 🟡 **MODERATE RISK** - Active partnership with product satisfaction concerns

**Key Risk:** Product bugs threatening user adoption; competitive alternatives being used

---

**Account Identification and Baseline**

**Company ID:** [REDACTED]

**Domain:** [company-domain.com]

**Account Type:** Strategic Partner + Customer

**Relationship Duration:** [START DATE] - Present ([X]+ months)

**Meeting Volume:** [X]+ recorded engagements

**Key Stakeholders Identified:**

- **[EXECUTIVE NAME]** (Board/Founder level) - [email@company.com]
- **[PRIMARY USER]** (Primary user/implementer) - [email@company.com]
- **[TECHNICAL LEAD]** (Systems architect/AI lead) - [email@company.com]
- **[PARTNERSHIP LEAD]** (Partnership/Marketing) - [email@company.com]

---

**Meeting Analysis Sources**

| Date | Meeting Title | Duration | Attendees | Upshot | Source |
| --- | --- | --- | --- | --- | --- |
| [DATE] | [Internal] x [Primary User] Sync | [X]:[X] | [Primary User], [Internal] | Product feedback session - multiple bugs identified | [X]% |
| [DATE] | [Executive]/[Internal]/[Primary User] | [X]:[X] | [Executive], [Internal], [Primary User], [Team Member] | Partnership alignment and AI agent development | [X]% |
| [DATE] | [Company]/[Our Company] - Catch-up | [X]:[X] | [Primary User], [Technical Lead], [Internal], [Internal] | Bug reports and UI improvement feedback | [X]% |
| [DATE] | [Internal] & [Product Lead] Showcase Sync | [X]:[X] | [Product Lead], [Internal] | Partner showcase event planning | [X]% |

---

**Meeting Engagement Analysis ([X]+ Day Period)**

**Meeting Frequency Trends:**

- **Peak Engagement:** [MONTH YEAR] ([X] meetings in [X] days)
- **Recent Activity:** [MONTH YEAR] ([X] critical feedback sessions)
- **Average Frequency:** [X]-[X] meetings per month
- **Engagement Quality:** High - technical depth and strategic discussions

**Stakeholder Participation Patterns:**

- **[Primary User]:** Primary power user and feedback provider ([X]/[X] meetings)
- **[Technical Lead]:** Technical implementer and systems architect ([X]/[X] meetings)
- **[Executive]:** Strategic advisor, sporadic but high-influence participation ([X]/[X] meetings)
- **[Partnership Lead]:** Partnership/marketing coordination ([X]/[X] meetings)

**Internal vs External Ratio:** [X]% external-inclusive meetings

---

**Sentiment and Satisfaction Tracking**

Sentiment Progression Over Time

**[PERIOD 1]: 🟢 POSITIVE**

- High enthusiasm for partnership potential
- Strong technical alignment and roadmap discussions
- Active collaboration on product development

**[PERIOD 2]: 🟡 NEUTRAL with CONCERNS**

- Technical integration challenges emerging
- Bug reports starting to accumulate
- Competing priorities around HubSpot deal management

**[PERIOD 3]: 🔴 FRUSTRATED**

- **Critical Quote:** "Users are utilizing alternative methods, like [Competitor], for summarizing meetings"
- **Key Issue:** "[Our Company]'s competitors, like [Competitor], provide better content quality"
- Multiple bugs affecting core functionality

**Support Issues and Resolution Patterns**

- **Deal Summary Bugs:** Multiple deals per company causing routing confusion
- **Recording Interruptions:** Breakout room functionality gaps
- **Data Mapping Issues:** Incorrect call-to-deal associations
- **Follow-up Email Quality:** Not meeting user expectations vs. competitors

**Feature Requests and Enhancement Discussions**

- Enhanced data mapping for multi-deal scenarios
- Improved summary content quality
- Better breakout room recording capabilities

… [example reduced for length]

</aside>

### SPICED Opportunity Matrix by Customer Account

**Prompt Name**: `spiced_opportunity_matrix_by_customer_account`

**Use for**: Customer retention strategy, expansion planning, renewal preparation, QBR insights

**Arguments**:

- `account_name` (required): Company name to analyze
- `analysis_period` (optional): Days of history to analyze (default: 180)

**Implementation**:

This prompt uses the following Grain MCP tools in sequence:

1. `search_companies` - Find company by name and get contacts
2. `list_meetings` - Get comprehensive meeting history
3. `search_persons` - Map stakeholder relationships
4. `fetch_meeting_notes` - Analyze sentiment and topics
5. `search_meetings` - Track specific themes and concerns

```markdown
Generate a complete SPICED analysis for customer account {account_name}:

Step 1: Account identification and meeting collection
- Search for company name to get company ID and all associated contacts
- Find all meetings with this customer (last {analysis_period} days)
- List participants, roles, and engagement frequency
- Create timeline of touchpoints and support interactions

Step 2: Meeting Analysis Sources table
Create a reverse chronological table with:
- Date, Meeting Title, Duration
- Attendees (exclude bot/notetaker names)
- Upshot: 15-word-or-less summary of purpose and outcome
- Source: Percentage indicating relative importance to customer SPICED analysis

Step 3: SITUATION analysis - Current state assessment
Document the customer's current state:
- Company size, growth, or contraction signals
- Organizational changes (mergers, leadership, restructuring)
- Current product usage patterns and adoption levels
- Integration touchpoints and workflow dependencies
- Team members actively using the solution
- Recent business initiatives or strategic shifts mentioned

Step 4: PAIN identification - Ongoing challenges
Analyze current and emerging customer pains:
- Unresolved technical issues or limitations
- New business challenges since implementation
- Process inefficiencies still present
- Feature gaps causing workarounds
- Support ticket patterns and escalations
- Competitive solutions being evaluated
- Change management struggles

Step 5: IMPACT assessment - Value realization
Measure achieved and potential impacts:
- Quantified value delivered to date
- ROI metrics shared by customer
- Success stories and wins attributed to solution
- Efficiency gains or cost savings realized
- Missed impact opportunities
- Expansion potential if pains addressed
- Risk of churn impact on their business

Step 6: CRITICAL EVENT mapping - Key dates ahead
Identify upcoming critical events:
- Contract renewal date and process
- Budget planning cycles
- Leadership or organizational changes
- Competitive RFP timelines mentioned
- Business seasonality affecting usage
- Product roadmap items they're waiting for
- Expansion project timelines

Step 7: DECISION dynamics - Renewal & expansion
Analyze decision-making for retention/growth:
- Current decision makers vs. original buyers
- New stakeholders to engage
- Budget authority changes
- Procurement process for renewals
- Expansion approval requirements
- Risk factors for non-renewal
- Champion strength and advocacy

Step 8: Customer health scoring
Create SPICED-based health assessment:
- Situation stability (organizational health)
- Pain severity (unresolved issues impact)
- Impact achievement (value realization score)
- Critical event preparedness
- Decision maker engagement level
- Overall retention risk rating

Step 9: Expansion opportunity analysis
Based on SPICED insights:
- Additional use cases to explore
- New teams/departments to engage
- Upsell opportunities aligned to pains
- Cross-sell potential based on impacts
- Reference and advocacy potential
- Case study opportunities

Step 10: Strategic account plan
Develop action plan from SPICED analysis:
- Immediate pain resolution priorities
- Executive business review preparation
- Renewal negotiation strategy
- Expansion conversation timing
- Relationship strengthening tactics
- Competitive defense strategies
- Success metric documentation needs

Include specific quotes showing satisfaction/concern levels, usage trends, and a visual SPICED health matrix.
```

<aside>
🌶️

[Redacted Example Output] **SPICED Customer Analysis: [Customer Name]**

| **SPICED Component** | **Status** | **Score** | **Key Insight** |
| --- | --- | --- | --- |
| **🏢 SITUATION** | Stable | [X]/10 | Mid-market consulting firm with advanced AI initiatives |
| **😣 PAIN** | High Impact | [X]/10 | Critical bugs affecting core workflows, data mapping issues |
| **💡 IMPACT** | Good Value | [X]/10 | Strong methodology implementation, unrealized potential |
| **⚡ CRITICAL EVENT** | Moderate Risk | [X]/10 | Champion transition, renewal timeline approaching |
| **👥 DECISION** | Strong | [X]/10 | High engagement, multiple stakeholders aligned |

**Overall Health Score: [X]/10** - Healthy customer with immediate technical attention needed

---

**Account Identification and Meeting Collection**

**Company:** [REDACTED CUSTOMER]

**Domain:** [REDACTED].com

**Company ID:** [REDACTED]

**Analysis Period:** [DATE RANGE REDACTED] (365 days)

**Total Customer-Relevant Meetings:** [X] meetings

**Key Stakeholders & Engagement Frequency**

- **[REDACTED A]** (Executive Chairman) - Strategic decision maker, [X] meetings
- **[REDACTED B]** (Product Manager) - Primary implementation lead, [X] meetings
- **[REDACTED C]** (Applied Math Student/Analyst) - Technical implementation, [X] meetings
- **[REDACTED D]** (Partnership Manager) - Partnership initiatives, [X] meetings

**Meeting Analysis Sources Table**

| Date | Meeting Title | Duration | Key Attendees | Upshot | Source (%) |
| --- | --- | --- | --- | --- | --- |
| [DATE] | [INTERNAL] x [CUSTOMER] Sync | [XX:XX] | [REDACTED], [INTERNAL] | Product feedback session identifying critical bugs | [XX]% |
| [DATE] | Intro: [CUSTOMER]/[INTERNAL]/[CUSTOMER] | [XX:XX] | [REDACTED], [REDACTED], [INTERNAL] | Partnership alignment and product enhancement discussion | [X]% |
| [DATE] | [CUSTOMER] x [COMPANY]: GTM Intelligence Agent Research | [XX:XX] | [REDACTED], [INTERNAL] | AI implementation strategy and customer interaction preferences | [X]% |
| [DATE] | [CUSTOMER]/[COMPANY] - Catch-up | [XX:XX] | [REDACTED], [REDACTED], [INTERNAL] | Bug fixes and data mapping improvements needed | [XX]% |

**Key Insights and Recommendations**

*"If there weren't bugs, I think it would all just be awesome. Like I'm super impressed with what I see and our users themselves are just. We need to get the bugs worked out."* - [CHAMPION]

*"I think [COMPETITOR] does a really good job... Their UI does not look nearly as good as yours, which I honestly think makes a big difference. But the summaries themselves that they produce or the follow up emails that they draft are like... it's just like, okay, yeah, that's totally."* - [CHAMPION]

The account represents a high-value strategic partnership with significant expansion potential, but immediate technical debt resolution is critical for retention and growth. The transition of [CHAMPION]'s role requires careful champion management while technical issues are addressed.

**SITUATION Analysis - Current State Assessment**

Company Profile

- **Size:** Mid-market B2B consulting/training company specializing in Revenue Architecture
- **Growth Stage:** Established with innovative AI initiatives (Project [REDACTED])
- **Organizational Structure:** Lean team with technical and business leadership
- **Current Usage:** Full team deployment with [X]+ recorded interactions

Current Product Integration Status

- **Primary Use Case:** SPICED methodology implementation across sales and customer success
- **Integration Points:** HubSpot CRM, Slack (planned), multiple AI agents
- **Team Adoption:** High engagement across sales, CS, and leadership teams
- **Technical Implementation:** Advanced with custom API integrations planned

Strategic Initiatives

- **Project [REDACTED]:** Internal AI agent system for customer intelligence
- **[REDACTED] AI Agent:** GTM Intelligence Agent for customer interaction management
- **Revenue Architecture Framework:** Bow-tie methodology extending beyond traditional sales

Partnership Development Timeline

- **Q4 [YEAR]:** Initial customer interest and early beta collaboration (November-December)
- **Q1 [YEAR]:** Official customer onboarding and advanced implementation (January-March)
- **Q2 [YEAR]:** Product feedback phase and technical debt identification (April-May)

**PAIN Identification - Ongoing Challenges**

Critical Technical Pains

1. **Multiple Deals Per Company Issue** (High Severity)
    - *Pain:* "We have multiple deals open with a given company. That makes it difficult when [PRODUCT] catches a call to know which deal to route it to"
    - *Frequency:* "Happens fairly frequently for us like because we will often do like a cross sell or upsell motion"
    - *Impact:* Causing confusion in deal tracking and misrouted summaries
2. **Data Mapping and Association Bugs** (High Severity)
    - *Pain:* "It'll just grab calls that are totally unrelated. Like it'll just grab in from like calls from other deals that are not linked to it"
    - *Impact:* Users creating workarounds with [COMPETITOR] for summaries
3. **Post-Close Tracking Limitation** (Medium Severity)
    - *Pain:* "After the deal is closed, we just stopped. [PRODUCT] just stops writing to the deal because it's closed"
    - *Impact:* Breaks continuity for customer success handoff

Process and User Experience Pains

1. **Breakout Room Recording Issues** (Medium Severity)
    - *Pain:* "When we jump into breakout rooms, [PRODUCT] just kind of assumes the meeting's over"
    - *Impact:* Missing critical discussions and incomplete meeting capture
2. **Content Quality Inconsistencies** (Medium Severity)

… [example reduced for length]

---

</aside>

---

## Sales Performance & Coaching

*Team-wide performance patterns and individual rep development*

### Sales Team Performance & Coaching Opportunities Report

**Prompt Name**: `sales_team_performance_coaching_opportunities_report`

**Use for**: Team training priorities, performance trends, systematic issues

**Arguments**:

- `analysis_days` (optional): Days of coaching data to analyze (default: 30)

**Implementation**:

This prompt uses the following Grain MCP tools in sequence:

1. `list_coaching_feedback` - Get meetings with coaching opportunities
2. `fetch_meeting_coaching_feedback` - Get detailed scores for each meeting
3. `list_workspace_users` - Map reps to their performance data
4. `search_meetings` - Find patterns in objections and successful calls

```markdown
Analyze sales performance and coaching needs over the last {analysis_days*} days:

Step 1: Coaching data collection
- Use list_*coaching_*feedback with has_*coaching_*opportunities filter to find flagged meetings
- Use fetch_*meeting_*coaching_*feedback to include overall scores and category breakdowns
- Focus on meetings with external participants (sales calls)

Step 2: Individual performance analysis:
- Use list_*workspace_*users to identify all reps
- Use fetch_*meeting_*coaching_*feedback to track score trends by rep over time
- Analyze weakest skill categories per person
- Review behavioral patterns (talk time, filler words)
- Identify consistent feedback themes

Step 3: Team-wide coaching priorities:
- Aggregate coaching feedback to find most common skill gaps across reps
- Identify systematic issues affecting multiple people
- Use search_meetings* to find best practice examples from high-scoring calls
- Extract role-play scenarios from real objections

Step 4: Development recommendations:
- Generate individual coaching plans with specific focus areas
- Prioritize team training needs with measurable outcomes
- Define success metrics and tracking methods
- Create timeline for improvement assessment

Include specific coaching feedback quotes and score progressions.
```

<aside>
👩‍🏫

[Redacted Example Output] **Scorecard Performance by Sales Rep (90 Days)**

Performance Summary Table

| Rep Name | Calls Assessed | Overall Avg | Rapport Building | Customer Qualification | Understanding Needs | Demonstrating Value | Objection Handling | Closing Ability | Performance Tier |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| **Rep A** | 25 | **3.1** | 3.2 | 2.9 | 3.8 | 3.3 | 3.7 | **2.4** | **Needs Improvement** |
| **Rep B** | 1 | **4.0** | 4.0 | 4.0 | 5.0 | 3.0 | 4.0 | 3.0 | **Good** |
| **Rep C** | 4 | **3.5** | 4.0 | 2.3 | 4.0 | 3.8 | 3.5 | 3.3 | **Good** |
| **Rep D** | 1 | **3.0** | 3.0 | 3.0 | 4.0 | 2.0 | 3.0 | **1.0** | **Needs Improvement** |
| **Rep E** | 3 | **3.7** | 3.7 | 3.3 | 4.0 | 4.3 | 4.0 | 3.7 | **Good** |

---

**Detailed Performance Analysis by Rep**

**Rep A** (Primary Sales Rep)

**Call Volume:** 25 assessed calls

**Risk Level:** HIGH - Primary rep with concerning closing performance

Scorecard Breakdown:

- **Rapport Building:** 3.2/5.0 - Inconsistent, frequent technical issues
- **Customer Qualification:** 2.9/5.0 - **Critical weakness**
- **Understanding Customer Needs:** 3.8/5.0 - **Strength**
- **Demonstrating Value:** 3.3/5.0 - Room for improvement
- **Objection Handling:** 3.7/5.0 - Generally competent
- **Closing Ability:** 2.4/5.0 - **CRITICAL WEAKNESS**

Performance Range:

- **Best Performance:** 4.0/5.0 (high-scoring demos)
- **Worst Performance:** 2.0/5.0 (renewal call)
- **Consistency Issue:** Wide variance indicates lack of standardized approach

Behavioral Patterns:

- **Technical Issues:** 40% of calls had connectivity problems affecting rapport
- **Self-Deprecating Tendency:** Multiple instances undermining credibility
- **Passive Closing:** Consistently fails to advance sales process

---

**Rep C** (Customer Success/Strategic)

**Call Volume:** 4 assessed calls

**Risk Level:** MEDIUM - Strong relationship skills, weak qualification

Strengths:

- **Rapport Building:** 4.0/5.0 - Excellent relationship building
- **Understanding Customer Needs:** 4.0/5.0 - Strong empathy and listening
- **Demonstrating Value:** 3.8/5.0 - Good at articulating benefits

Critical Weakness:

- **Customer Qualification:** 2.3/5.0 - **Significant gap in discovery process**

… [example reduced for length]

---

**Performance Tier Definitions**

**Good Performers (3.5+ Average)**

- **Rep E:** 3.7 - Coaching demo specialist
- **Rep C:** 3.5 - Customer success focused
- **Rep B:** 4.0 - Limited data but promising

**Adequate Performers (3.0-3.4 Average)**

- None currently in active sales roles

**Needs Improvement (<3.0 or Critical Weaknesses)**

- **Rep A:** 3.1 - **PRIMARY CONCERN** due to closing weakness and high call volume
- **Rep D:** 3.0 - **SUPPORT ROLE ONLY** due to closing inability

---

**Critical Insights**

Volume vs. Performance Risk

- **Rep A:** Handles 83% of assessed calls but has critical closing weakness
- **Revenue Impact:** Primary rep's 2.4 closing score is costing deals

Skills Distribution

- **Strongest Team Skill:** Understanding Customer Needs (3.8 average)
- **Weakest Team Skill:** Closing Ability (2.9 average)
- **Biggest Individual Gap:** Rep A's qualification and closing skills

… [example reduced for length]

</aside>

---

# Frequently Asked Questions

**Q: What applications and platforms support MCP integrations?**

**A:** The Model Context Protocol is rapidly gaining adoption where each client supports different MCP features (tools, prompts, resources) depending on their use cases. For the semi-complete list of Clients with feature compatibility details, visit the [official MCP clients directory](https://modelcontextprotocol.io/clients).

**Q: What Claude plan do I need to use MCP integrations?**

**A:** MCP integrations, including the Grain MCP server, are only available on paid Claude plans (Pro, Team, and Enterprise). Free Claude accounts do not support MCP integrations or the ability to connect external tools and data sources. You'll need to upgrade to a paid plan to access the Grain integration and other MCP servers.

**Q: Are all Grain MCP tools available on every Grain plan?**

**A:** Most Grain MCP tools work on all Grain plans (Free, Starter, Business, Enterprise), including meeting search, transcripts, notes, and contact management. However, tools for Deals (`list_open_deals`, `list_all_deals`, `fetch_deal`) and Sales Coaching/Scorecards (`list_coaching_feedback`, `fetch_meeting_coaching_feedback`) are restricted to Business and Enterprise plan users only. Free and Starter plan users will receive an error if they attempt to use these premium tools.

**Q: Is it safe to use MCP servers like Grain's?**

**A:** MCP security relies on a trust model, and Grain's MCP server is officially supported by us and aligns with our existing security practices, follows the MCP specification exactly, and uses industry-standard OAuth authentication and HTTPS. All tool usage requires explicit user approval in Claude, and each tool request is scoped to specific data needed for that operation. While no system is 100% secure, Grain's established security practices and transparent approach to data handling make it a safer MCP implementation.

**Q: How does the Model Context Protocol (MCP) work and what are the privacy implications?**

**A:** The Model Context Protocol (MCP) is an open standard that creates a secure bridge between Claude and external services like Grain, where your data stays in your Grain account and is only processed temporarily by Claude to answer questions. As stated by [Anthropic](https://www.anthropic.com/news/integrations), data accessed through MCP integrations is not used to train Claude's models.

**Q: What data does Grain's MCP server have access to?**

**A:** Grain's MCP server only accesses data you already have permission to view in your Grain workspace, including meetings you attended, companies and contacts from those meetings, deal information (with HubSpot integration), and AI-generated notes and transcripts. It has no access to private meetings you weren't invited to or other workspaces you don't belong to. The integration uses OAuth authentication and maintains the same security boundaries as your normal Grain usage.

**Q: How does Claude verify and approve MCP tool usage?**

**A:** Claude requires explicit user approval before using any Grain tool, showing you a dialog with clear descriptions of what each tool will do and offering "use once" or "use for entire session" options. Each tool requires separate approval when first used, and you maintain control over which tools Claude can access in your current session. You can revoke access by starting a new chat session, ensuring that no tools run without your explicit permission.

**Q: Can I control what data the Grain MCP server shares with Claude?**

**A:** Data access is controlled through your existing Grain account permissions, and you can enable/disable specific tools in Claude's integration settings, but you cannot currently exclude specific meetings or companies from MCP access. The integration accesses all data you have permission to see in your Grain workspace and follows your existing permissions rather than providing additional filtering options. Review your Grain workspace permissions before connecting and use targeted prompts to limit the scope of data Claude requests.

**Q: What is the `helpful_usage_information` parameter I see in the client's tool responses?**

**A:** You may notice the `helpful_usage_information` parameter appearing in chat interface when the Grain MCP server responds to tool requests. This optional parameter helps Grain's team understand tool usage patterns to improve functionality, and this data is never used as AI training data. Currently there's no opt-out option, but one will be available in the coming months - if you're uncomfortable with this data collection, consider waiting until then.
