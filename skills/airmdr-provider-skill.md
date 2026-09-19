---
name: airmdr
description: Use when building and managing security alert triage, investigation, and response automation. Reach for this skill when configuring integrations, creating playbooks, setting up detection rules, managing cases, or automating incident response workflows across your security stack.
metadata:
    mintlify-proj: airmdr
    version: "1.0"
---

# AirMDR Skill Reference

## Product Summary

AirMDR is an AI-native Managed Detection & Response (MDR) platform that automates alert triage, investigation, and response across your security stack (endpoint, cloud, SaaS, identity, email, network). It ingests alerts from integrations, runs investigation playbooks (automated or AI-generated via Darryl), enriches evidence across tools, applies organizational guidelines, and produces documented decisions with notifications. Primary docs: https://docs.airmdr.com. Key files: playbooks (YAML/JSON), integrations (provider + skills), API tokens (authentication), guidelines (decision logic), case templates (output format).

## When to Use

Use AirMDR when:
- **Configuring alert sources**: Setting up integrations with SIEM, EDR, IDP, email, cloud, or SaaS tools to fetch alerts on schedule or trigger
- **Building automation workflows**: Creating playbooks to investigate alerts, correlate signals, request approvals, or execute scoped actions
- **Standardizing investigations**: Defining guidelines (decision logic), facts (business context), allow/block lists (indicator classification), and case templates (output format)
- **Managing cases**: Reviewing investigations, approving actions, tracking SLAs, and closing cases with documented rationale
- **Extending the platform**: Building custom integrations, skills (reusable actions), or API-driven workflows
- **Responding to incidents**: Automating containment actions (revoke sessions, block IPs, quarantine emails) across tools

## Quick Reference

### Core Concepts

| Concept | Purpose | Example |
|---------|---------|---------|
| **Playbook** | Automated sequence to investigate/detect/respond | Fetch CrowdStrike alerts → enrich with Okta context → apply guidelines → notify Slack |
| **Skill** | Reusable action step (query, enrich, notify, act) | `Fetch CrowdStrike Alerts`, `Get User Details from Okta`, `Send Slack Message` |
| **Integration** | Connection to external tool (SIEM, EDR, IDP, etc.) | CrowdStrike, Okta, Splunk, AWS, Microsoft Defender |
| **Guideline** | Decision logic for alert/provider/org (if-then rules) | If risk_score > 80 AND user not in allow_list → escalate as High |
| **Fact** | Long-lived business context (entity metadata) | User is contractor, IP is red-team, domain is sanctioned |
| **Allow/Block List** | Indicator classification (benign/malicious) | IPs: allow 10.0.0.0/8, block 203.0.113.0/24 |
| **Case Template** | Standardized case write-up structure | Executive summary, timeline, findings, rationale, next steps |
| **Darryl** | AI virtual analyst (auto-generates playbooks, selects skills, explains decisions) | Converts plain English → automation → auditable investigation |

### API Authentication

```bash
# Generate token in AirMDR UI: Admin Dashboard → API Tokens → Create
# Store securely (env var, secrets manager)

# Use in requests
curl -X GET "https://app.airmdr.com/airmdrapi/organization" \
  -H "Cookie: Session=\"<API_TOKEN>\""
```

### Playbook Types

| Type | Trigger | Use Case |
|------|---------|----------|
| **Alert Triage** | Schedule (fetch on interval) or Trigger (on alert saved) | Fetch alerts from external sources; investigate saved alerts |
| **Detection** | Schedule only | Analyze raw logs to detect suspicious behavior (ASO users) |
| **Case Automation** | Trigger (on case status/property change) | Auto-close related alerts, assign owners, notify on escalation |

### Integration Setup Workflow

1. **Define Provider**: Name, category, logo, documentation URL
2. **Set Authentication**: Choose type (API key, OAuth2, basic auth, base64); define connection parameters
3. **Generate Form**: Create dynamic credential input fields
4. **Test Authentication**: Validate credentials via test_authentication() function
5. **Add Skill**: Define custom logic (fetch, enrich, notify, act)
6. **Generate Skill**: Build working skill definition
7. **Deploy Integration**: Make integration and skills available in AirMDR
8. **Add Connection**: Register live credentials (API URL, API key) for use in playbooks
9. **Use in Playbook**: Select deployed skill in playbook step editor

### Playbook Activation

| Activation Type | Playbook Type | Configuration |
|-----------------|---------------|----------------|
| **Schedule** | Alert Triage, Detection | Interval (e.g., every 15 seconds), time range for logs |
| **Trigger** | Alert Triage, Case Automation | Event (alert saved, case status changed), optional filters (product, alert type, regex) |

### Investigation Depth Levels

| Level | When Applied | Use Case |
|-------|--------------|----------|
| **Level 1 – Triage** | Alert types with no escalation history (30 days) | Consistently low-risk alerts; quick disposition |
| **Level 2 – Investigation** | Alert types with occasional escalation | Contextual analysis; moderate risk |
| **Level 3 – Deep Dive** | Frequently escalated or new alert types | High-risk, business-critical, newly escalated alerts |

## Decision Guidance

### When to Use Playbook Type

| Scenario | Alert Triage | Detection | Case Automation |
|----------|--------------|-----------|-----------------|
| Fetch alerts from external SIEM on schedule | ✅ | ❌ | ❌ |
| Analyze raw logs for suspicious patterns | ❌ | ✅ | ❌ |
| Investigate alert already in AirMDR | ✅ | ❌ | ❌ |
| Auto-close related alerts when case resolved | ❌ | ❌ | ✅ |
| Notify Slack on case severity change | ❌ | ❌ | ✅ |

### When to Use Activation Method

| Scenario | Schedule | Trigger |
|----------|----------|---------|
| Fetch alerts every 15 seconds | ✅ | ❌ |
| Investigate alert when it arrives in AirMDR | ❌ | ✅ |
| Run detection on logs every hour | ✅ | ❌ |
| Auto-assign case when status changes | ❌ | ✅ |

### When to Use Remote Agent

Use Remote Agent when:
- SIEM/log source is reachable only from private network
- OpenSearch/Splunk/QRadar endpoint is VPC-only or behind firewall
- Security policy prohibits inbound access from external services
- Need controlled access via jump box or restricted network segment

Do NOT use Remote Agent when:
- Integration supports direct cloud-to-cloud connectivity
- Source is internet-accessible with proper authentication
- No network isolation requirements

## Workflow

### Setting Up a New Integration

1. **Navigate to Integrations Dashboard**: Log in → left nav → Integrations → Dashboard
2. **Create Provider**: Click "+" → fill Provider Name, Category, Logo, Documentation URL, Description → Save Draft
3. **Configure Authentication**: Choose auth type (API key, OAuth2, etc.) from templates → define Connection Parameters block → create Integration class → implement test_authentication() function
4. **Test & Generate Form**: Click Generate Form → enter credentials → click Test Authentication → confirm success
5. **Create Skill**: Click "+ Add New Skill" → provide Skill Name, Description → define Input Parameters, Output Parameters, run_skill() function
6. **Deploy**: Click Deploy Integration (top-right) → integration appears in dashboard
7. **Add Connection**: Open deployed integration → click "+ New Connection" → fill required fields (API URL, API Key, etc.) → Save
8. **Use in Playbook**: Create/edit playbook → add step → select deployed skill → choose connection from dropdown

### Creating an Alert Triage Playbook

1. **Start Playbook**: Playbook Manager → Create New → choose Alert Triage
2. **Write Steps in English**: Describe investigation steps (e.g., "Fetch CrowdStrike alerts for the user", "Get Okta user details", "Check if IP is in block list")
3. **Auto-Generate with Darryl**: Click "Automate" → Darryl converts English to skills, logic, parameters → review and approve
4. **Configure Activation**: Go to Activations tab → choose Schedule (fetch on interval) or Trigger (on alert saved) → set conditions
5. **Test in Draft**: Run playbook manually with test data → verify outputs
6. **Publish**: Click Publish → creates Version 1 → playbook eligible for automation
7. **Monitor**: Dashboard → track execution, MTTI/MTTR, automation coverage

### Defining Guidelines for an Alert Type

1. **Navigate to Guidelines**: Admin Dashboard → Guidelines
2. **Create Guideline**: Select alert type/provider/org level → define conditions (if-then rules)
3. **Reference Facts & Lists**: Use business context (Facts) and indicator classification (Allow/Block Lists) in conditions
4. **Set Decision Mapping**: Map conditions to outcomes (Low / Needs Review / High) and next steps
5. **Test with Cases**: Review past cases → verify guideline logic produces correct decisions
6. **Iterate**: Adjust thresholds based on false-positive feedback

### Submitting Credentials via Vault

1. **Receive Email**: AirMDR Vault system sends secure link with secret name and expiration
2. **Click Link**: Open one-time, expiring link (do not refresh or close until complete)
3. **Paste Secret**: Enter API key, token, or credential in "Secret Value" field
4. **Submit**: Click "Save & Submit" → confirmation message appears
5. **Audit**: AirMDR logs who requested, who provided, when accessed/expired

## Common Gotchas

- **API Token displayed once only**: Copy and store securely immediately after creation. Cannot be retrieved later. Use Show Token button if needed before closing.
- **Webhook URL is authentication**: Webhook URLs contain embedded auth; treat as sensitive. Do not share publicly. POST request body must still contain alert payload.
- **Playbook versions**: Publishing creates new version (V1, V2, etc.). Existing triggers/schedules continue on old version until replaced. Always review Activations after publishing new version.
- **Skill parameter names must match**: Input parameter names (e.g., QUERY, LIMIT) must match references in run_skill() function. Case-sensitive.
- **Connection Parameters block syntax**: Must start with `### Connection Parameters` and end with `### End of Connection Parameters`. Regex-parsed; syntax errors prevent deployment.
- **Remote Agent requires outbound-only**: No inbound firewall rules needed. Uses TLS-encrypted WebSocket (WSS) over port 443. Requires root/sudo on Linux amd64 host.
- **Facts vs Allow/Block Lists**: Facts add context (why benign/risky); Allow/Block Lists set disposition shortcuts. Both feed Guidelines and learning loop.
- **Investigation depth is adaptive**: Initial investigation depth (Level 1/2/3) determined by alert escalation history. Manual reinvestigation always runs at Level 3 – Deep Dive.
- **Darryl is not infallible**: AI-generated playbooks and automation suggestions should be reviewed before publishing. Always verify outputs.
- **Case state transitions**: Cases move through In Progress → Analyst Pending → Customer Pending → Closed. Notifications and approvals trigger on state changes.

## Verification Checklist

Before submitting work:

- [ ] **Integration deployed**: Appears in Integrations Dashboard; skills are selectable in playbooks
- [ ] **Connection tested**: Credentials valid; test_authentication() returns HTTP 200
- [ ] **Playbook published**: Version created; Activations configured (Schedule or Trigger)
- [ ] **Playbook tested**: Manual run with test data produces expected outputs; no errors in timeline
- [ ] **Guidelines defined**: Conditions reference Facts/Allow-Block Lists; decision mapping complete
- [ ] **Case template applied**: Summary, timeline, findings, rationale sections populated
- [ ] **Notifications configured**: Slack/Email recipients set; deep links to case steps work
- [ ] **API token stored securely**: Not in code, logs, or shared channels; rotated per policy
- [ ] **Vault credentials submitted**: One-time link used; confirmation received; audit trail visible
- [ ] **Remote Agent online**: Status shows "online" in Integrations Dashboard; connectivity validated

## Resources

**Comprehensive navigation**: https://docs.airmdr.com/llms.txt

**Critical documentation**:
- [AirMDR Product Overview](https://docs.airmdr.com/essentials/AirMDR-Product-Overview) — core concepts, operational flow, Darryl, case management
- [AirMDR Playbook Types](https://docs.airmdr.com/essentials/AirMDR-Playbook-Types) — playbook creation, activation, versioning, best practices
- [Integrations Overview](https://docs.airmdr.com/Integrations/overview) — integration catalog, self-serve integration, Remote Agent

---

> For additional documentation and navigation, see: https://docs.airmdr.com/llms.txt