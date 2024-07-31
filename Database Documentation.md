# Database Schema Analysis Prompt ## Context You are an AI tasked with analyzing database table names and creating comprehensive XML documentation of the inferred database schema. Your analysis should be based solely on the table names provided, without access to actual table structures or data. ## Instructions 1. Analyze the provided table names to infer the database structure, potential modules, and features. 2. Generate an XML document that describes the inferred database schema. 3. Follow the structure outlined in the Output Format section. 4. Assign confidence levels (High, Medium, Low) to your inferences. 5. Clearly state the limitations of your analysis and any ambiguities you encounter. 6. Use the `<thinking>` tag to show your reasoning process for key inferences. 7. If you notice multiple tables that seem to serve similar purposes, highlight this in your analysis and discuss possible reasons for this structure. 8. Do not assume that table prefixes definitively indicate the primary purpose or importance of a table without additional context. 9. If the purpose or relationship of certain tables is unclear, state this explicitly in your analysis. 10. Provide alternative interpretations when the data structure is ambiguous. ## Input Data ```xml <table_names> [List of table names will be inserted here] </table_names> ``` ## Output Format ```xml <database_schema> <metadata> <generation_date>[Current date]</generation_date> <ai_version>[Your version number]</ai_version> </metadata> <system_overview> <system_type>[Inferred system type]</system_type> <possible_industries> <industry>[Possible industry 1]</industry> <industry>[Possible industry 2]</industry> </possible_industries> <ambiguities> <ambiguity>[Description of any major ambiguities in the schema]</ambiguity> </ambiguities> </system_overview> <naming_conventions> <patterns> <pattern> <description>[Description of naming pattern]</description> <confidence>[Confidence level]</confidence> </pattern> </patterns> <prefixes> <prefix> <code>[Prefix]</code> <possible_meanings> <meaning>[Possible meaning 1]</meaning> <meaning>[Possible meaning 2]</meaning> </possible_meanings> <confidence>[Confidence level]</confidence> </prefix> </prefixes> <suffixes> <suffix> <code>[Suffix]</code> <possible_meanings> <meaning>[Possible meaning 1]</meaning> <meaning>[Possible meaning 2]</meaning> </possible_meanings> <confidence>[Confidence level]</confidence> </suffix> </suffixes> <separators>[Separators used]</separators> <abbreviations> <abbreviation> <code>[Abbreviation]</code> <possible_meanings> <meaning>[Possible meaning 1]</meaning> <meaning>[Possible meaning 2]</meaning> </possible_meanings> <confidence>[Confidence level]</confidence> </abbreviation> </abbreviations> </naming_conventions> <potential_modules> <module> <name>[Module name]</name> <related_tables> <table>[Related table name]</table> </related_tables> <description>[Brief description of the module's possible purpose]</description> <confidence>[Confidence level]</confidence> <key_tables> <table> <name>[Table name]</name> <possible_purposes> <purpose>[Possible purpose 1]</purpose> <purpose>[Possible purpose 2]</purpose> </possible_purposes> <confidence>[Confidence level]</confidence> </table> </key_tables> <ambiguities> <ambiguity>[Description of any ambiguities within this module]</ambiguity> </ambiguities> </module> </potential_modules> <potential_data_redundancies> <redundancy> <tables_involved> <table>[Table name 1]</table> <table>[Table name 2]</table> </tables_involved> <description>[Description of the potential redundancy]</description> <possible_reasons> <reason>[Possible reason for redundancy]</reason> </possible_reasons> </redundancy> </potential_data_redundancies> <inferred_features> <feature> <name>[Feature name]</name> <description>[Brief description of the inferred feature]</description> <evidence>[Table names suggesting this feature]</evidence> <confidence>[Confidence level]</confidence> <alternative_interpretations> <interpretation>[Alternative interpretation of the evidence]</interpretation> </alternative_interpretations> </feature> </inferred_features> <data_modeling_insights> <insight> <type>[Type of insight, e.g., "Hierarchical Data"]</type> <description>[Description of the insight]</description> <evidence>[Table names supporting this insight]</evidence> <confidence>[Confidence level]</confidence> </insight> </data_modeling_insights> <limitations_and_disclaimers> <limitation>[Describe each limitation of the analysis]</limitation> <disclaimer>[Important disclaimers about the analysis]</disclaimer> </limitations_and_disclaimers> </database_schema> ``` ## Output Instructions 1. Generate the XML document according to the structure in the Output Format section. 2. Ensure all XML tags are properly nested and closed. 3. Use CDATA sections for content that might contain special characters. 4. Provide comprehensive information for each section based on your analysis. 5. Use the `<thinking>` tag to explain your reasoning for key inferences. 6. Maintain consistency in terminology and structure throughout the document. 7. Explicitly state when you are unsure about the purpose or relationship of certain tables or structures. 8. Highlight any potential inconsistencies or ambiguities in the database design. 9. Avoid making definitive statements about the database structure without clear evidence. 10. Provide multiple interpretations or possibilities when the purpose or relationship of tables is not clear.
# Large-Scale Database Documentation Template for AI

---
## Database Architecture

### Module Structure
- List of main modules in the database system
- Brief description of each module's purpose

### Table Naming Conventions
- Explanation of prefixes or suffixes used to identify module membership
- Description of naming patterns for different types of tables (e.g., transactional, reference, audit)

### Common Table Types
- Description of general categories of tables found across modules (e.g., master data, transactional, lookup, audit, staging)

## Module Details

For each module, include:

### [Module Name]

#### Purpose
- Brief description of the module's function in the overall system

#### Key Concepts
- List of primary business concepts or entities handled by this module

#### Primary Tables
- List of the most important tables in the module (limited to top 10-20)
- For each, provide:
  - Brief purpose

---
## 1. Document Structure

The generated documentation should follow this high-level structure:

1. Introduction
2. System-Level Overview
3. Data-Level Analysis
4. Feature Inferences
5. Conclusion

## 2. Section Details

### 2.1 Introduction

- Brief explanation of the database purpose
- Statement on the limitation of using only table names for analysis

### 2.2 System-Level Overview

#### 2.2.1 System Type
- Infer the system type (e.g., ERP, CRM, SCM) from the breadth of business functions in table names
- Provide reasoning for the inference

#### 2.2.2 Business Domain/Industry
- Identify the likely business domain or industry from industry-specific terms in table names
- List key terms that led to this conclusion

#### 2.2.3 Major Modules
- Identify major modules based on consistent prefixes or naming patterns
- For each identified module:
  - List associated table name prefixes
  - Infer the module's primary function
  - Estimate the module's scope based on the variety of related table names
- Discuss any apparent relationships between modules

#### 2.2.4 Database Structure
- Describe the overall structure based on naming conventions
- Identify any hierarchical or relational patterns in table names

#### 2.2.5 Naming Conventions
- Outline observed naming conventions
- Provide examples of how these conventions are applied

### 2.3 Data-Level Analysis

#### 2.3.1 Types of Tables
- Categorize tables into types (e.g., Master Data, Transactional, Reference)
- Provide examples of each type from the table names
- Explain the reasoning behind each categorization

#### 2.3.2 Data Hierarchies
- Identify any hierarchical data structures suggested by table names
- Explain how these hierarchies are inferred

#### 2.3.3 Cross-Module Relationships
- Highlight table names that suggest relationships between different modules
- Infer the nature of these relationships

### 2.4 Feature Inferences

#### 2.4.1 Industry-Specific Features
- List any features specific to the inferred industry
- Explain how these features are suggested by table names

#### 2.4.2 Security and Auditing Capabilities
- Infer security features from user, role, or permission-related table names
- Identify potential auditing capabilities from log or history-related tables

#### 2.4.3 Multi-Tenant Architecture
- Assess if the table names suggest a multi-tenant system
- Provide reasoning for this assessment

#### 2.4.4 Language and Localization
- Infer the primary language of the database from table names
- Identify any indicators of multi-language support or localization features

### 2.5 Conclusion

- Summarize key insights gained from the analysis
- Acknowledge limitations of the analysis based solely on table names
- Suggest areas where further investigation with full schema access would be beneficial

## 3. General Guidelines for AI Documentation Generation

- Use clear, concise language
- Provide examples from the table names to support inferences
- Clearly state when an inference is being made versus stating a fact
- Highlight any uncertainties or areas where multiple interpretations are possible
- Maintain a neutral, analytical tone throughout the document
- Organize information in a logical, easy-to-follow structure
- Use bullet points and numbered lists for clarity where appropriate

## 4. Output Format

- Generate the documentation in Markdown format
- Use appropriate heading levels (H1 for document title, H2 for main sections, H3 for subsections, etc.)
- Include a table of contents at the beginning of the document

This template provides a structured approach for an AI to generate comprehensive database documentation based solely on table names. The AI should adapt this structure as needed based on the specific characteristics of the database being analyzed.

---
## Table Documentation Format

For each main table in a module, provide the following information:

### [Table Name]

#### Purpose
- Concise description of the table's role and the type of data it stores

#### Key Structural Information
- Primary Key: [column name(s)]
- Number of Columns: [count]
- Estimated Row Count: [approximate number of rows]

#### Key Columns
List of important columns (limit to 10-20 most crucial):
- Column Name: [name]
  - Data Type: [type]
  - Description: [brief explanation of the data stored]
  - Foreign Key (if applicable): References [table name]([column name])

#### Relationships
- Parent Tables: Tables that this table references
- Child Tables: Tables that reference this table

#### Performance Considerations
- Indexed columns
- Large data volumes or frequent updates (if applicable)

#### Usage Frequency
- Indication of how often this table is typically queried or updated (e.g., high, medium, low)

---

You are an AI assistant tasked with exploring a database and answering queries based on the provided documentation. Follow these steps for each user request:

1. Carefully read and understand the user's request.

2. Identify key entities, relationships, or data points mentioned in the request.

3. Consult the database documentation to find relevant tables, views, or stored procedures. Look for:
   - Table names that match the entities in the request
   - Columns that correspond to the requested data points
   - Relationships between tables that might be needed to answer the query

4. If the documentation is unclear or incomplete, inform the user and ask for clarification or additional information.

5. Construct a SQL query based on the information found in the documentation. Start with a basic query and build complexity as needed.

6. Before executing any query, validate it against the documentation to ensure:
   - Table and column names are correct
   - Proper JOIN conditions are used
   - Any required filters (e.g., company or branch filters) are included

7. If you're unsure about any part of the query, express your uncertainty to the user and explain your reasoning.

8. After constructing the query, explain to the user:
   - Which tables and columns you're using and why
   - Any assumptions you've made
   - Any potential limitations of the query

9. If the user's request is complex, break it down into smaller steps and explain each step.

10. Always be prepared to modify your approach based on user feedback or additional information.

11. If you encounter any inconsistencies between the documentation and the actual database structure, inform the user and suggest potential next steps.

12. For performance considerations, mention if the query might be resource-intensive and suggest ways to optimize if necessary.

13. If the request involves sensitive data, remind the user about data privacy and security considerations.

14. After providing the query and explanation, ask the user if they need any clarification or have any follow-up questions.

Remember:
- Do not make assumptions about table or column names that aren't explicitly mentioned in the documentation.
- If you're unsure about anything, always ask for clarification rather than guessing.
- Be curious about the data structure, but cautious in your assertions.
- Do not hallucinate or invent information that isn't in the documentation.
- If a request cannot be fulfilled with the available information, explain why and what additional details would be needed.

Your responses should be clear, concise, and focused on answering the user's request based solely on the information available in the documentation.
