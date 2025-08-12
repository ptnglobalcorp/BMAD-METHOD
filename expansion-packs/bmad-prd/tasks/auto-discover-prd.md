# Auto Discover PRD Task

## Purpose

To intelligently search and retrieve Product Requirements Documents (PRDs) from all configured MCP sources based on user-provided criteria. This task performs comprehensive discovery across multiple systems to find the most relevant requirements without requiring users to know specific source locations or identifiers.

## Task Instructions

You are now operating as an Intelligent PRD Discovery Specialist. Your goal is to gather user criteria, search across all available MCP sources, and retrieve the most relevant product requirements in a comprehensive, consolidated format.

### SEQUENTIAL Task Execution (Do not proceed until current Task is complete)

### 1. Elicit Discovery Criteria from User

#### 1.1 Gather Primary Search Criteria (Required)

Present numbered options and collect user input:

```markdown
# PRD Auto-Discovery - Criteria Collection

To find the most relevant product requirements, please provide:

## Primary Information (Required)

1. **Product/Project Name**: What product or project are you looking for?
2. **Feature/Component**: Specific feature, component, or area of focus?
3. **Timeframe**: When should these requirements be from?
   - Current/Active requirements
   - Specific date range
   - Latest version only
   - Historical requirements

Please provide at least the Product/Project Name to begin discovery.
```

Wait for user response before proceeding.

#### 1.2 Gather Additional Context (Optional)

If user wants more targeted results, collect:

```markdown
## Additional Filters (Optional - Enter 'skip' to use defaults)

4. **Requirement Type**:
   - User Stories
   - Technical Specifications
   - API Requirements
   - Business Rules
   - All Types
5. **Priority Level**:
   - High priority only
   - Medium and above
   - All priorities
6. **Status Filter**:
   - Active/In Progress
   - Ready for Development
   - All statuses
7. **Keywords**: Any specific terms or phrases to search for?

8. **Exclude Sources**: Any systems to skip during search?
```

#### 1.3 Confirm Discovery Scope

Present summary for user confirmation:

```markdown
## Discovery Configuration

- **Product**: {product_name}
- **Feature**: {feature_name or "All"}
- **Timeframe**: {timeframe}
- **Types**: {requirement_types}
- **Priority**: {priority_filter}
- **Status**: {status_filter}
- **Keywords**: {keywords or "None"}
- **Excluded Sources**: {excluded_sources or "None"}

Proceed with auto-discovery? (y/n)
```

### 2. Load All Available MCP Sources

#### 2.1 Discover Active Sources

- Use `list-external-resources.md` to identify all configured MCP servers and their available PRD sources
- Look at all configured MCP servers and their tools
- Identify all available PRD sources (Jira, Confluence, PDFs, Word docs, etc.)

#### 2.2 Create Search Strategy

Organize sources by search capability:

**Text-Based Search Sources:**

- Jira (JQL queries)
- Confluence (CQL queries)
- Document systems (full-text search)
- Knowledge bases (content search)

**Structured Query Sources:**

- Databases (SQL queries)
- REST APIs (parameter-based filtering)
- GraphQL endpoints (field-specific queries)

**File-Based Sources:**

- Document repositories (filename/metadata search)
- Version control systems (commit message search)
- Shared drives (file content search)

### 3. Execute Multi-Source Discovery

#### 3.1 Construct Source-Specific Queries

**For Jira Sources:**

```yaml
search_strategy: "comprehensive_jql"
queries:
  - base: "project = '{project}' AND text ~ '{product_name}'"
  - feature: "summary ~ '{feature_name}' OR description ~ '{feature_name}'"
  - type: "issueType IN (Story, Epic, Requirement, Bug)"
  - priority: "priority >= '{priority_threshold}'" # if specified
  - status: "status IN ({status_list})" # if specified
  - keywords: "text ~ '{keyword1}' OR text ~ '{keyword2}'"
  - timeframe: "updated >= '{start_date}' AND updated <= '{end_date}'"
combined_jql: "{base} AND ({feature}) AND ({type}) [AND ({priority})] [AND ({status})] [AND ({keywords})] [AND ({timeframe})]"
```

**For Confluence Sources:**

```yaml
search_strategy: "content_query_language"
queries:
  - space_filter: "space.key = '{space}' OR space.name ~ '{product_name}'"
  - content_filter: "title ~ '{feature_name}' OR text ~ '{product_name}'"
  - type_filter: "type = page AND label IN (requirements, prd, specification)"
  - date_filter: "lastModified >= '{start_date}'"
combined_cql: "({space_filter}) AND ({content_filter}) AND ({type_filter}) [AND ({date_filter})]"
```

**For Document Sources:**

```yaml
search_strategy: "file_content_search"
parameters:
  filename_patterns: ["*{product_name}*", "*requirements*", "*prd*", "*spec*"]
  content_keywords:
    ["{product_name}", "{feature_name}", "requirements", "acceptance criteria"]
  file_types: ["pdf", "docx", "md", "txt"]
  date_range: "{start_date}" # if specified
  exclude_patterns: ["backup*", "*temp*", "*draft*"] # unless drafts requested
```

#### 3.2 Execute Parallel Search Operations

- Launch concurrent searches across all active sources
- Implement timeout handling (60 seconds per source)
- Collect results as they arrive
- Handle partial failures gracefully
- Log search performance metrics

#### 3.3 Real-Time Progress Reporting

Display live progress updates:

```markdown
# Auto-Discovery in Progress...

✅ Jira Production: Found 23 items (2.3s)
✅ Confluence KB: Found 15 pages (3.1s)
🔄 SharePoint Docs: Searching... (8.2s)
⚠️ Internal API: Timeout - partial results (30.0s)
❌ Legacy Database: Connection failed
✅ GitHub Repos: Found 7 files (5.8s)

Total Progress: 5/6 sources complete
```

### 4. Analyze and Consolidate Results

#### 4.1 Result Aggregation

Combine results from all sources:

- Normalize data formats across different source types
- Remove exact duplicates based on content similarity
- Merge related items (e.g., story and its tasks)
- Preserve source attribution for each item

#### 4.2 Relevance Scoring Algorithm

Score each item based on:

**Content Relevance (40%)**

- Exact product name matches: +20 points
- Feature name in title: +15 points
- Feature name in content: +10 points
- Keyword matches: +5 points each
- Related terms: +2 points each

**Recency Score (25%)**

- Last 30 days: +25 points
- Last 90 days: +20 points
- Last 6 months: +15 points
- Last year: +10 points
- Older: +5 points

**Priority/Status Score (20%)**

- High priority: +20 points
- Medium priority: +15 points
- Active status: +15 points
- Ready status: +10 points
- Other statuses: +5 points

**Source Reliability (15%)**

- Primary sources (Jira, official docs): +15 points
- Secondary sources (wiki, shared docs): +10 points
- Cached/backup sources: +5 points

#### 4.3 Intelligent Deduplication

- Identify near-duplicate content using content similarity
- Group related items (parent/child relationships)
- Merge information from multiple sources about the same requirement
- Preserve version history and source diversity

### 5. Organize and Present Comprehensive Results

#### 5.1 Result Categorization

Organize findings into logical groups:

**By Requirement Type:**

- User Stories and Epics
- Technical Specifications
- API Requirements
- Business Rules and Constraints
- Testing Requirements

**By Development Phase:**

- Active Development
- Ready for Development
- In Review/Approval
- Backlog/Planning
- Archived/Completed

**By Source System:**

- Primary Requirements (Jira, official PRDs)
- Supporting Documentation (Confluence, wikis)
- Technical Specifications (code repos, API docs)
- Research and Analysis (user research, market analysis)

#### 5.2 Generate Discovery Report

Using `{root}/templates/prd-output-tmpl.yaml`, create comprehensive report:

```yaml
discovery_metadata:
  search_criteria:
    product: "{product_name}"
    feature: "{feature_name}"
    timeframe: "{search_timeframe}"
    filters_applied: ["{filter_list}"]
  execution_stats:
    sources_searched: {source_count}
    sources_successful: {success_count}
    total_items_found: {total_count}
    search_duration_seconds: {duration}
    relevance_threshold: {min_score}

consolidated_results:
  high_relevance: # Score >= 70
    - title: "{requirement_title}"
      source: "{source_system}"
      relevance_score: {score}
      type: "user_story" | "technical_spec" | "api_requirement"
      priority: "high" | "medium" | "low"
      status: "{current_status}"
      last_updated: "{timestamp}"
      summary: "{brief_description}"

  medium_relevance: # Score 40-69
    - title: "{requirement_title}"
      # ... same structure

  related_content: # Score 20-39
    - title: "{related_item_title}"
      # ... same structure
```

#### 5.3 Present Interactive Results

Display results with numbered options for user interaction:

```markdown
# PRD Auto-Discovery Results

## Search Summary

- **Criteria**: {product_name} > {feature_name}
- **Sources Searched**: {success_count} of {total_count}
- **Total Items Found**: {total_items}
- **High Relevance**: {high_count} | **Medium**: {medium_count} | **Related**: {related_count}
- **Search Duration**: {duration}s

## High Relevance Results ({high_count} items)

### 1. **{title}** (Score: {score})

- **Source**: {source_system} | **Type**: {type}
- **Priority**: {priority} | **Status**: {status}
- **Updated**: {last_updated}
- **Summary**: {brief_summary}
- **Actions**: View Details | Fetch Full Content | Add to Export

### 2. **{title}** (Score: {score})

- **Source**: {source_system} | **Type**: {type}
- **Summary**: {brief_summary}
- **Actions**: View Details | Fetch Full Content | Add to Export

## Medium Relevance Results ({medium_count} items)

[Collapsed - Type 'expand medium' to show all]

## Related Content ({related_count} items)

[Collapsed - Type 'expand related' to show all]

## Discovery Issues

⚠️ {issue_count} sources had partial or failed results:

- Internal API: Connection timeout
- Legacy Database: Authentication failed

## Next Actions

1. **Fetch All High Relevance** - Retrieve full content for top results
2. **Custom Selection** - Choose specific items to fetch
3. **Expand Search** - Modify criteria and search again
4. **Export Current Results** - Save discovery report
5. **Manual Source Search** - Search specific source with \*fetch-prd

Enter action number or 'help' for more options:
```

### 6. Handle User Interaction and Follow-up

#### 6.1 Process User Selection

Support these interaction patterns:

- **Number Selection**: Fetch full content for selected item
- **Range Selection**: "1-5" fetches items 1 through 5
- **Action Commands**: "expand medium", "fetch all high", "export results"
- **Refinement**: "refine search", "add criteria", "exclude source"

#### 6.2 Fetch Selected Content

For user-selected items:

- Execute targeted `fetch-specific-prd` operations
- Combine results into consolidated PRD document
- Maintain source attribution and metadata
- Present unified view of all selected requirements

#### 6.3 Support Iterative Refinement

If results are not satisfactory:

```markdown
## Refine Discovery

Current results not meeting your needs? Let's refine:

1. **Expand Search Scope**:
   - Include more sources
   - Broaden keyword matching
   - Extend date range

2. **Narrow Search Focus**:
   - Add more specific keywords
   - Filter by requirement type
   - Limit to specific sources

3. **Adjust Relevance**:
   - Lower relevance threshold
   - Change priority weighting
   - Include archived content

What would you like to adjust?
```

### 7. Generate Comprehensive Output Package

#### 7.1 Create Multi-Format Export

Generate complete package including:

- **Executive Summary**: Discovery overview and key findings
- **Detailed Results**: Full content for selected items
- **Source Attribution**: Complete traceability to original sources
- **Search Metadata**: Criteria, sources, and performance metrics
- **Quality Assessment**: Completeness and reliability indicators

#### 7.2 Save Discovery Session

Cache all results for future reference:

- Save search criteria and results to `{root}/data/auto-discovery-{timestamp}.yaml`
- Create quick-access shortcuts for high-relevance items
- Update source performance and reliability metrics
- Log successful search patterns for future optimization

## Expected Output

1. **Interactive Results Display**: Scored and categorized findings with user options
2. **Comprehensive PRD Package**: Consolidated requirements from multiple sources
3. **Discovery Report**: Search metadata, performance, and quality assessment
4. **Cached Session**: Saved results and criteria for future reference
5. **Follow-up Options**: Clear next steps and refinement opportunities

## Error Handling and Fallbacks

- **No Results Found**: Suggest criteria refinement or manual source exploration
- **Partial Source Failures**: Continue with available sources, report issues
- **Low Relevance Scores**: Lower thresholds or expand search scope
- **System Overload**: Implement queuing and progressive loading
- **Data Quality Issues**: Flag problems and suggest alternative sources

## Integration Points

- Seamlessly transition to `fetch-specific-prd.md` for detailed content retrieval
- Support `export-requirements.md` for comprehensive output formatting
- Integrate with `list-mcp-resources.md` for source discovery and management
- Connect with BMad-Method story creation workflows for requirement integration
