# Fetch Specific PRD Task

## Purpose

Retrieve product requirements from specified external sources using available tools and capabilities. This task accepts a source identifier and detail/key parameter to fetch targeted PRD content and present it in a structured, actionable format for BMad-Method workflows.

## Task Parameters

- **source**: Tool identifier, MCP server name, or resource key that maps to available capabilities (required)
- **detail/key**: Specific item identifier, filter criteria, or search parameters for targeted retrieval (required)

## Task Instructions

You are now executing the Fetch Specific PRD task. Your goal is to retrieve specific product requirements from the designated source using your available tools and present them in a structured, user-friendly format.

### SEQUENTIAL Task Execution (Complete each step before proceeding)

### 1. Parameter Analysis and Validation

#### 1.1 Parse Input Parameters

**Source Parameter Processing:**

- Examine the provided `source` parameter
- Map source to your available tools and capabilities
- Identify the appropriate tool/method for this source type

**Detail/Key Parameter Processing:**

- Parse the `detail/key` parameter for the specified source context
- Understand what specific content needs to be retrieved
- Prepare parameters in the format expected by the identified tool

#### 1.2 Tool Capability Assessment

**CRITICAL**: Before proceeding, verify you have the appropriate tools available:

```markdown
## Tool Availability Check

Checking available capabilities for source: `{source}`

Available tools that might work:

- [List relevant tools you have access to]
- [Note any missing capabilities]
```

**If NO appropriate tool is available:**

```markdown
❌ **No Compatible Tool Found**

I don't have access to source: `{source}`

**Recommended Next Steps:**

1. Use `*list-resources` to see all available sources and tools
2. Use `*auto-fetch-prd` to let me search across all available sources
3. Provide a different source that matches my available capabilities

Please select an option (1-3) or provide more details about the source.
```

### 2. Tool Execution and Content Retrieval

#### 2.1 Execute Appropriate Tool

**Based on identified tool, execute retrieval:**

For each tool type, construct appropriate parameters:

- Format detail/key according to tool requirements
- Set appropriate filters, limits, and options
- Include error handling for failed requests

#### 2.2 Handle Retrieval Results

**Successful Retrieval:**

- Parse and validate returned content
- Assess completeness of the retrieved data
- Identify any follow-up retrievals needed

**Failed or Partial Retrieval:**

```markdown
⚠️ **Content Retrieval Issue**

Could not retrieve content for: `{source}` with key: `{detail/key}`

**Possible Reasons:**

- Key/detail not found in source
- Insufficient permissions
- Source temporarily unavailable
- Invalid key format

**Recommended Next Steps:**

1. Use `*list-resources` to verify available content in this source
2. Try `*auto-fetch-prd` with search terms instead of specific keys
3. Retry with a different detail/key value
4. Check source access and permissions

Please select an option (1-4) or provide corrected parameters.
```

### 3. Content Analysis and Enhancement Assessment

#### 3.1 Evaluate Retrieved Content

**Assess what was retrieved:**

- Identify content type (user stories, requirements, epics, etc.)
- Check for completeness and missing elements
- Determine if additional fetches are needed for full context

#### 3.2 Additional Content Discovery

**If content references related items:**

```markdown
## Related Content Discovered

The retrieved PRD references additional items:

- Related Epic: PROJ-456
- Dependent Stories: PROJ-789, PROJ-012
- Architecture Doc: ARCH-123

**Fetch Additional Content?**

1. Yes, fetch all related items automatically
2. Let me select specific items to fetch
3. No, proceed with current content only

Please select (1-3):
```

### 4. Present Retrieved Content

#### 4.1 Format Content for Display

**Present in structured markdown format:**

```markdown
# 📄 PRD Content Retrieved

## Source Information

- **Source**: {source_identifier}
- **Retrieved**: {timestamp}
- **Content Type**: {type_of_content}
- **Status**: ✅ Complete | ⚠️ Partial | 🔄 Additional content available

---

## 📋 Requirements Summary

### {Main_Title}

{main_description}

### 🎯 User Stories ({count})

**Story ID: {story_id}** - Priority: {priority}

- **Title**: {story_title}
- **Description**: {story_description}
- **Acceptance Criteria**:
  - ✓ {criteria_1}
  - ✓ {criteria_2}
  - ✓ {criteria_3}
- **Story Points**: {points} | **Status**: {status}

[Repeat for each story...]

### 🔧 Technical Requirements

- **API Requirements**: {api_details}
- **Data Models**: {data_models}
- **Integration Points**: {integrations}
- **Performance Criteria**: {performance}

### 📐 Business Rules & Constraints

- {business_rule_1}
- {business_rule_2}
- {constraint_1}

### 📎 Attachments & References

- 📄 [{attachment_name}]({attachment_url}) - {description}
- 🔗 [{reference_name}]({reference_url}) - {description}

---

## 🎯 Content Quality Assessment

- **Completeness**: {percentage}% complete
- **Missing Elements**: {list_missing_items}
- **Recommendation**: {quality_recommendation}
```

### 5. Provide Next Action Options

**Always present numbered options for user selection:**

```markdown
## 🚀 Next Steps

**What would you like to do next?**

1. **Export this content** - Save PRD to file using `*export-prd`
2. **Fetch related content** - Retrieve additional referenced items
3. **Search for more** - Use `*auto-fetch-prd` to find related content
4. **Try different source** - Use `*list-resources` to see other options
5. **Refetch with different key** - Retry current source with new detail/key
6. **Switch to analysis mode** - Enter `*chat-mode` for discussion

**Please select an option (1-6) or ask questions about the retrieved content.**
```

### 6. Error Handling and Fallbacks

#### 6.1 Tool Not Available

- Guide user to `*list-resources` command
- Suggest `*auto-fetch-prd` as alternative
- Provide clear error message with next steps

#### 6.2 Content Not Found

- Verify parameters with user
- Suggest alternative search approaches
- Offer to list available content in source

#### 6.3 Partial Success

- Present available content clearly
- Mark missing sections
- Offer options to complete retrieval

### 7. Maintain BMad-Method Alignment

#### 7.1 Agent Behavior Principles

- **Tools-First Integration**: Always leverage available tools before manual alternatives
- **Numbered Options Protocol**: Every choice presented as numbered list
- **User-Guided Discovery**: Help users understand and select from available options
- **Error Resilience**: Handle failures gracefully with clear next steps
- **Quality Validation**: Always assess and report on content completeness

#### 7.2 Workflow Integration

- Ensure retrieved content is ready for export via `*export-prd`
- Support follow-up with `*auto-fetch-prd` for broader search
- Enable resource discovery through `*list-resources`
- Maintain conversation flow with clear status updates

## Expected Output Format

1. **Parameter validation** with tool availability check
2. **Retrieval execution** with success/failure handling
3. **Structured content presentation** in beautiful markdown
4. **Quality assessment** with completeness metrics
5. **Numbered next-step options** for continued workflow
6. **Error handling** with clear guidance and alternatives

## Success Criteria

- User parameters correctly parsed and validated
- Appropriate tool identified and executed successfully
- PRD content retrieved and formatted beautifully
- Quality assessment provided with clear metrics
- User presented with clear, numbered next-step options
- All error conditions handled with helpful guidance
- Content ready for export or further processing
