---
name: project-documentation
description: Create high-quality README and system documentation for software projects. Use cases: (1) Writing or updating project README documentation, (2) Adding system operation principle flowcharts (Mermaid), (3) Writing detailed step-by-step usage instructions, (4) Organizing and optimizing configuration descriptions (environment variables, config files), (5) Making documentation more user-friendly and easier to understand. Applicable to any scenario requiring improved project documentation, especially open-source projects, internal tools, and API services.
---

# Project Documentation

Create clear, complete, and user-friendly README and system documentation for software projects.

## Core Capabilities

This skill helps you create high-quality project documentation including:

1. **Mermaid Flowcharts** - Visualize system operation principles
2. **Step-by-Step Usage Instructions** - Detailed beginner guides
3. **Configuration Documentation** - Clear organization of environment variables and config files

## Workflow

### 1. Understand the Project

Before writing documentation, understand the project's core content:

**Essential Information**:
- What are the project's core features?
- What is the tech stack? (frontend, backend, database, external services)
- How do users use this project? (startup process, core operations)
- What external dependencies are needed? (API Keys, accounts, tools)
- What configuration items exist? (required vs optional)

**Information Gathering Methods**:
- Read existing README (if available)
- Check package.json or similar dependency config files
- Review .env.example or config files
- Examine main code files (e.g., main.ts, app.ts, routes/)
- Ask users for key information

### 2. Create Mermaid Flowcharts

Choose appropriate flowcharts based on project type:

#### Core Flow Diagram (Required)
Shows the complete flow from user startup to completing core tasks.

**When to Use**: All projects should have a core flow diagram.

**Reference Template**: See "Core Flow Diagram" section in [references/mermaid-patterns.md](references/mermaid-patterns.md).

**Key Elements**:
- Starting point: User starts system
- Decision points: Login verification, config checks, etc.
- Core operations: Main feature flows
- Endpoint: Task completion or return to main interface

#### Data Flow Diagram (Recommended)
Shows interaction sequence between system components.

**When to Use**:
- Projects with separated frontend and backend
- Projects involving multiple service interactions
- Projects requiring API call flow explanation

**Reference Template**: See "Data Flow Diagram" section in [references/mermaid-patterns.md](references/mermaid-patterns.md).

**Key Elements**:
- Participants: User, frontend, backend, database, external services
- Interaction numbering: Number each step
- Request-response: Clearly mark data flow direction

#### Technical Architecture Diagram (Recommended)
Shows system tech stack and layered structure.

**When to Use**:
- Projects with complex tech stacks
- Projects requiring system architecture explanation
- Multi-layered architecture projects

**Reference Template**: See "Technical Architecture Diagram" section in [references/mermaid-patterns.md](references/mermaid-patterns.md).

**Key Elements**:
- Layers: Frontend layer, backend layer, data layer, external services layer
- Technology labels: Specific frameworks and tools
- Dependencies: Arrows indicate dependency direction

**Complete Mermaid Templates and Best Practices**: Read [references/mermaid-patterns.md](references/mermaid-patterns.md)

### 3. Write Step-by-Step Usage Instructions

Organize usage steps according to the following structure:

#### Prerequisites
List what users need to prepare:
- Software dependencies (Node.js, Python, etc., including version requirements)
- Package managers (npm, pnpm, pip, etc.)
- External accounts (if needed)
- Other tools

#### Standard Step Sequence
1. **Clone project and install dependencies**
2. **Obtain external service credentials** (if needed)
3. **Configure environment variables**
4. **Initialize system** (if needed)
5. **Start services**
6. **Use features**
7. **Verify system operation**

#### Standard Format for Each Step
```markdown
### Step N: Verb-led Title

Brief explanation of this step's purpose (1-2 sentences).

1. Specific operation 1
2. Specific operation 2
3. Specific operation 3

\`\`\`bash
# If commands are needed, provide complete copy-paste commands
command --option value
\`\`\`

**Expected Output**:
\`\`\`
Expected output content
\`\`\`

> 💡 **Tip**: Additional notes or tricks
> ⚠️ **Note**: Common errors or precautions
```

**Complete Step Writing Guide**: Read [references/step-by-step-guide.md](references/step-by-step-guide.md)

### 4. Organize Configuration Documentation

#### .env.example File Structure

Use clear separators and grouping:

```bash
# ========================================
# Main Category Title
# ========================================
CONFIG_ITEM=example_value

# ----------------------------------------
# Subcategory Title
# ----------------------------------------
CONFIG_ITEM=example_value
```

#### Configuration Documentation in README

**Required Configuration Items**:
- Clearly mark as "required"
- Provide acquisition method
- Give complete examples
- Explain purpose

**Optional Configuration Items**:
- Clearly mark as "optional"
- Explain functional impact
- Provide default values
- Give configuration examples

**Multi-Option Configuration**:
- Use tables to compare different options
- Provide complete configuration examples for each option
- Explain applicable scenarios
- Mark recommended options

**Complete Configuration Organization Guide**: Read [references/config-organization.md](references/config-organization.md)

### 5. Documentation Structure Recommendations

Recommended README structure:

```markdown
# Project Name - Brief Description

> One sentence explaining the project's core functionality

## Features

- ✅ Feature 1
- ✅ Feature 2
- ✅ Feature 3

## System Operation Principles

### Core Flow Diagram
[Mermaid Core Flow Diagram]

### Data Flow Diagram
[Mermaid Data Flow Diagram]

### Technical Architecture Diagram
[Mermaid Technical Architecture Diagram]

## Quick Start (Step by Step)

### Prerequisites
[Prerequisites checklist]

### Step 1: ...
[Detailed steps]

### Step 2: ...
[Detailed steps]

...

## Common Commands

[Common commands list]

## API Examples

[API usage examples]

## Tech Stack

[Tech stack list]

## Project Structure

[Directory structure description]

## Documentation

[Other documentation links]

## Important Notes

[Precautions and risk warnings]

## License

[License information]
```

## Quality Checklist

After completing documentation, verify quality using the following checklist:

### Flowchart Check
- [ ] Core flow diagram clearly shows user operation flow
- [ ] Data flow diagram accurately reflects system interactions
- [ ] Technical architecture diagram completely shows tech stack
- [ ] All diagrams use appropriate colors and styles
- [ ] Diagram complexity is moderate (no more than 20 nodes)

### Usage Steps Check
- [ ] Prerequisites checklist is complete
- [ ] Each step has clear title and purpose explanation
- [ ] Complete copy-paste commands provided
- [ ] Expected output or results explained
- [ ] Common problem tips included
- [ ] Step sequence matches actual operation flow

### Configuration Documentation Check
- [ ] Required and optional configuration items clearly categorized
- [ ] Each configuration item has purpose explanation
- [ ] Detailed steps provided for obtaining external service credentials
- [ ] Config files use clear separators and grouping
- [ ] Multi-option configurations have comparison and recommendations

### User-Friendliness Check
- [ ] Clear icons used (✅ ⚠️ 💡)
- [ ] Multiple option choices provided (if applicable)
- [ ] Troubleshooting tips included
- [ ] Language is concise and easy to understand
- [ ] All external links are accessible

## Reference Resources

This skill includes the following reference documents, read as needed:

- **[mermaid-patterns.md](references/mermaid-patterns.md)** - Mermaid flowchart design patterns and templates
- **[step-by-step-guide.md](references/step-by-step-guide.md)** - Step-by-step usage instruction writing guide
- **[config-organization.md](references/config-organization.md)** - Configuration documentation organization guide

## Common Scenarios

### Scenario 1: Create README for New Project

1. Use Glob/Read tools to understand project structure
2. Check package.json, .env.example, and other config files
3. Create core flow diagram, data flow diagram, technical architecture diagram
4. Write detailed step-by-step usage instructions
5. Organize configuration documentation
6. Verify using quality checklist

### Scenario 2: Update Existing README

1. Read existing README
2. Identify missing or unclear parts
3. Add Mermaid flowcharts (if missing)
4. Optimize usage steps (add expected output, tips, etc.)
5. Reorganize configuration documentation (use separators, grouping)
6. Verify using quality checklist

### Scenario 3: Optimize Configuration Files

1. Read existing .env.example
2. Group configuration items by function
3. Add clear separators and comments
4. Mark required vs optional
5. Provide acquisition method links
6. Add detailed configuration documentation in README

## Best Practices

1. **User Perspective First** - Start from the perspective of a completely new user unfamiliar with the project
2. **Actionability** - All commands should be directly copy-pasteable
3. **Completeness** - Include all necessary information, don't skip key steps
4. **Clarity** - Use diagrams, tables, code blocks to improve readability
5. **Verifiability** - Provide verification steps to let users confirm successful operations

## Important Notes

- Don't assume users have any background knowledge
- Don't skip any steps
- Don't use vague descriptions (like "configure environment variables properly")
- Don't omit expected output or verification steps
- Don't forget to add common problem tips
