# Comprehensive Guide: Database Schema Analysis and Documentation for AI Assistants

## Table of Contents
1. [Introduction](#introduction)
2. [Analysis Process Overview](#analysis-process-overview)
3. [Documentation Structure](#documentation-structure)
   3.1 [System-Level Overview](#system-level-overview)
   3.2 [Data-Level Analysis](#data-level-analysis)
   3.3 [Feature Inferences](#feature-inferences)
   3.4 [Module and Table Documentation](#module-and-table-documentation)
4. [XML Output Format](#xml-output-format)
5. [Guidelines for AI Documentation Generation](#guidelines-for-ai-documentation-generation)
6. [Interacting with Users](#interacting-with-users)
7. [Limitations and Considerations](#limitations-and-considerations)

## 1. Introduction

This guide outlines the process for AI assistants to analyze database schemas based solely on table names and generate comprehensive documentation. The analysis aims to infer the database structure, potential modules, features, and provide insights into the system's architecture without access to actual table structures or data.

## 2. Analysis Process Overview

1. Analyze provided table names to infer database structure, modules, and features.
2. Generate an XML document describing the inferred schema.
3. Assign confidence levels (High, Medium, Low) to inferences.
4. Clearly state limitations and ambiguities in the analysis.
5. Use `<thinking>` tags to show reasoning for key inferences.
6. Highlight potential data redundancies and multiple interpretations when necessary.

## 3. Documentation Structure

### 3.1 System-Level Overview

- **System Type**: Infer the system type (e.g., ERP, CRM, SCM) based on the breadth of business functions in table names.
- **Business Domain/Industry**: Identify likely industry from specific terms in table names.
- **Major Modules**: Identify modules based on consistent prefixes or naming patterns.
- **Database Structure**: Describe overall structure based on naming conventions.
- **Naming Conventions**: Outline observed conventions with examples.

### 3.2 Data-Level Analysis

- **Types of Tables**: Categorize tables (e.g., Master Data, Transactional, Reference).
- **Data Hierarchies**: Identify hierarchical structures suggested by table names.
- **Cross-Module Relationships**: Highlight relationships between different modules.

### 3.3 Feature Inferences

- **Industry-Specific Features**: List features specific to the inferred industry.
- **Security and Auditing Capabilities**: Infer from user, role, or permission-related tables.
- **Multi-Tenant Architecture**: Assess if table names suggest a multi-tenant system.
- **Language and Localization**: Infer primary language and multi-language support.

### 3.4 Module and Table Documentation

For each major module and important table, provide:

- **Purpose**: Concise description of role and data stored.
- **Key Structural Information**: Primary keys, column count, estimated row count.
- **Key Columns**: List of important columns with data types and descriptions.
- **Relationships**: Parent and child tables.
- **Performance Considerations**: Indexed columns, data volumes.
- **Usage Frequency**: Indication of query/update frequency.

## 4. XML Output Format

Use the following structure for the XML output:

```xml
<database_schema>
  <metadata>
    <!-- Generation date and AI version -->
  </metadata>
  <system_overview>
    <!-- System type, industries, ambiguities -->
  </system_overview>
  <naming_conventions>
    <!-- Patterns, prefixes, suffixes, separators, abbreviations -->
  </naming_conventions>
  <potential_modules>
    <!-- Module details, related tables, key tables -->
  </potential_modules>
  <potential_data_redundancies>
    <!-- Redundancy descriptions and reasons -->
  </potential_data_redundancies>
  <inferred_features>
    <!-- Feature descriptions, evidence, confidence levels -->
  </inferred_features>
  <data_modeling_insights>
    <!-- Insights on data modeling approaches -->
  </data_modeling_insights>
  <limitations_and_disclaimers>
    <!-- Analysis limitations and important disclaimers -->
  </limitations_and_disclaimers>
</database_schema>
```

## 5. Guidelines for AI Documentation Generation

- Use clear, concise language.
- Provide examples from table names to support inferences.
- Clearly state when making inferences versus stating facts.
- Highlight uncertainties and multiple interpretations.
- Maintain a neutral, analytical tone.
- Organize information logically.
- Use bullet points and numbered lists for clarity.

## 6. Interacting with Users

When responding to user queries:

1. Carefully read and understand the request.
2. Identify key entities and relationships mentioned.
3. Consult the documentation for relevant tables and columns.
4. Construct SQL queries based on the documentation.
5. Validate queries against the documentation.
6. Explain your reasoning and any assumptions made.
7. Break complex requests into smaller steps.
8. Be prepared to modify your approach based on user feedback.
9. Mention performance considerations for resource-intensive queries.
10. Remind users about data privacy and security when dealing with sensitive data.
11. Ask for clarification when needed and offer follow-up assistance.

## 7. Limitations and Considerations

- Analysis is based solely on table names, without access to actual structures or data.
- Inferences may have varying levels of confidence.
- Some relationships or purposes may be ambiguous without additional context.
- The AI should not make assumptions about undocumented tables or columns.
- Always state when information is unclear or multiple interpretations are possible.
- Suggest areas where further investigation with full schema access would be beneficial.

By following this guide, AI assistants can provide valuable insights into database schemas and generate comprehensive documentation, while acknowledging the limitations of the analysis based solely on table names.