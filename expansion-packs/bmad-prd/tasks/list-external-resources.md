# List External Resources

## Task Overview

**Purpose**: Discover and catalog all available external sources for fetching Product Requirements Documents (PRDs) using available tools and integrations.

**Agent**: prd (Product Requirements Fetcher)

**When to Use**: When user needs to see what PRD sources are available before fetching requirements.

## Task Instructions

### Step 1: Capability Assessment

1. **Inventory Available Tools**:
   - Examine all available tools and integrations in your current environment
   - Focus on tools that can connect to external systems for document/data retrieval
   - These capabilities are typically provided via Model Context Protocol (MCP) servers or direct integrations
   - DO NOT focus on local files or current workspace files.

2. **Reference Common Sources**:
   - Use the `common-prd-resources.md` data file as your baseline catalog
   - Cross-reference your available tools with the comprehensive list of PRD source types
   - Prioritize tools that align with common PRD storage locations

### Step 2: Resource Discovery Process

For each available tool/integration, discover accessible resources:

1. **Project Management Systems**:
   - Query available projects, boards, workspaces, or repositories
   - List project keys, workspace names, or board identifiers
   - Examples: Jira projects, Azure DevOps projects, Trello boards, Asana workspaces

2. **Documentation Platforms**:
   - Discover available spaces, pages, sites, wikis, or knowledge bases
   - You can search to list some spaces, pages, or wiki instances
   - List space names, site collections, or wiki instances. You don't need to list all pages, just the top-level spaces or sites.
   - Examples: Confluence spaces, Notion workspaces, SharePoint sites

3. **File Systems and Cloud Storage**:
   - Explore accessible directories, folders, or drives
   - Focus on common PRD storage locations (docs/, requirements/, specs/, shared/)
   - Examples: Remote allowed directories, Google Drive folders, OneDrive directories

4. **Code Repositories**:
   - List accessible repositories, organizations, or projects
   - Include both public and private repositories if available
   - Examples: GitHub repos, GitLab projects, Azure Repos

5. **Other Integrated Sources**:
   - Query any additional tools for accessible content
   - Include CRM systems, survey platforms, or collaboration tools
   - Examples: Salesforce instances, Google Forms, Slack workspaces

### Step 3: Generate Structured Report

Create a comprehensive report using this exact format:

```markdown
# External PRD Available Resources

## [Tool/Platform Name 1]

- Resource 1 Name
- Resource 2 Name
- Resource 3 Name

## [Tool/Platform Name 2]

- Resource A Name
- Resource B Name

[Continue for all discovered tools and resources]

## Next Steps Options

1. **Fetch PRD from specific resource** - Select a resource to fetch requirements
2. **Auto-discover PRD content** - Search all resources for PRD-related documents
3. **Refresh resource list** - Re-scan all tools for updated resources
```

### Step 4: Present User Options

Always conclude with numbered options following BMad's interaction protocol:

- Present choices as a numbered list
- Keep options clear and actionable
- Maintain context for follow-up actions
- Allow users to select by number

## Key Principles

1. **No Connection Testing**: Assume all available tools are functional - focus on discovery, not validation
2. **Comprehensive Discovery**: Query each available tool thoroughly for accessible resources
3. **Structured Presentation**: Use consistent markdown formatting for easy scanning
4. **User-Centric Options**: Provide clear next steps aligned with typical PRD fetching workflows

## Error Handling

- If no tools are available: "No external resource tools found. Please check your environment configuration."
- If tools exist but no resources found: List the tools with "No accessible resources" notation
- If discovery fails for specific tools: Note the tool with "Discovery failed - tool may need configuration"

## Success Criteria

- Complete inventory of all discoverable PRD sources organized by tool/platform
- Clear, scannable markdown format matching the specified structure
- Numbered options for immediate user action
- No assumptions about resource accessibility - just list what's discoverable

## Output Template

```markdown
# External PRD Available Resources

## [Discovered Tool/Platform]

- [Resource 1]
- [Resource 2]
- [etc.]

## Next Steps Options

1. **Fetch PRD from specific resource** - Select a resource to fetch requirements
2. **Auto-discover PRD content** - Search all resources for PRD-related documents
3. **Refresh resource list** - Re-scan all tools for updated resources
```
