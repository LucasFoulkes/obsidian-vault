## programs that already do this. 
## steps

- pick folder (directory) (using fzf like but with python)
- get all files (explore tree) make it into a list of paths for every file. also consider exisiting extructure or organisation
- 
## organiszational models 

### Scenario:
You're a small business owner managing files related to multiple business operations, such as marketing, finances, product development, customer support, and personal files related to your hobbies and travel.

### 1. **PARA Model**

#### Folder Structure:
```
/Projects
    /New Product Launch
        /Product_Design_Draft.png
        /Marketing_Plan.docx
        /Launch_Event_Invitation.pdf
    /Website Redesign
        /New_Layout_Mockup.png
        /SEO_Strategy.docx
        /Contract_With_Designer.pdf

/Areas
    /Business Finances
        /2024_Budget.xlsx
        /Tax_Records_2023.pdf
    /Customer Support
        /Support_Policy_Document.docx
        /Customer_Feedback_Analysis.xlsx

/Resources
    /Marketing Resources
        /Social_Media_Guide.pdf
        /Content_Calendar_Template.xlsx
    /Travel Guides
        /Europe_Trip_Itinerary.docx
        /Best_Food_Destinations.pdf

/Archives
    /Completed Projects
        /Q1_2023_Marketing_Campaign/
            /Final_Report.pdf
            /Completed_Ad_Designs.zip
    /Old Receipts
        /2019_Receipts/
            /Office_Supplies_2019.pdf
            /Software_Purchases_2019.xlsx
```

### 2. **MOC (Map of Content)**

#### Folder Structure:
```
/Main_MOC.md
    - [Business Operations](./Business_Operations_MOC.md)
    - [Personal Life](./Personal_Life_MOC.md)

/Business_Operations_MOC.md
    - [New Product Launch](./Projects/New_Product_Launch_MOC.md)
    - [Website Redesign](./Projects/Website_Redesign_MOC.md)
    - [Business Finances](./Areas/Business_Finances_MOC.md)

/Personal_Life_MOC.md
    - [Travel Plans](./Travel_Plans_MOC.md)
    - [Hobbies](./Hobbies_MOC.md)

/Projects
    /New_Product_Launch_MOC.md
        - Links to: Product_Design_Draft.png, Marketing_Plan.docx
    /Website_Redesign_MOC.md
        - Links to: New_Layout_Mockup.png, Contract_With_Designer.pdf

/Areas
    /Business_Finances_MOC.md
        - Links to: 2024_Budget.xlsx, Tax_Records_2023.pdf
```

### 3. **P.A.S.T.E. Framework**

#### Folder Structure:
```
/Projects
    /New Product Launch
        /Product_Design_Draft.png
        /Marketing_Plan.docx
        /Launch_Event_Invitation.pdf
    /Website Redesign
        /New_Layout_Mockup.png
        /SEO_Strategy.docx
        /Contract_With_Designer.pdf

/Areas
    /Business Finances
        /2024_Budget.xlsx
        /Tax_Records_2023.pdf

/Support
    /Marketing Resources
        /Social_Media_Guide.pdf
        /Content_Calendar_Template.xlsx

/Tasks
    /Task_Lists
        /Product_Development_Task_List.xlsx
        /Website_Redesign_Tasks.docx

/Energy
    /Hobbies
        /Photography_Tutorials/
            /Nature_Photography_Guide.pdf
            /Camera_Settings_Cheat_Sheet.png
```

### 4. **Archives Model**

#### Folder Structure:
```
/Current Projects
    /New Product Launch
        /Product_Design_Draft.png
        /Marketing_Plan.docx
        /Launch_Event_Invitation.pdf
    /Website Redesign
        /New_Layout_Mockup.png
        /SEO_Strategy.docx
        /Contract_With_Designer.pdf

/Active Areas
    /Business Finances
        /2024_Budget.xlsx
        /Tax_Records_2023.pdf
    /Customer Support
        /Support_Policy_Document.docx
        /Customer_Feedback_Analysis.xlsx

/Reference Materials
    /Marketing Resources
        /Social_Media_Guide.pdf
        /Content_Calendar_Template.xlsx

/Archived
    /Completed Projects
        /Q1_2023_Marketing_Campaign/
            /Final_Report.pdf
            /Completed_Ad_Designs.zip
    /Old Receipts
        /2019_Receipts/
            /Office_Supplies_2019.pdf
            /Software_Purchases_2019.xlsx
```

### Summary:
- **PARA Model**: Best for organizing ongoing projects, areas of responsibility, and keeping resources and archives clearly separated.
- **MOC**: Excellent for creating interconnected maps that link various aspects of your business and personal life, allowing for easy navigation through complex file structures.
- **P.A.S.T.E. Framework**: Ideal for organizing files according to projects, support materials, actionable tasks, and personal energy or focus-related files.
- **Archives**: Focused on differentiating between current, active, reference, and archived files, ensuring that old projects and inactive files are neatly stored away.

This approach provides tailored folder structures for managing diverse file types related to different areas of life and work, allowing for efficient organization and easy retrieval.

Yes, there are more modern and emerging models for organizing files and information, especially with the rise of digital tools and AI-driven technologies. These models focus on adaptability, automation, and integration with digital workflows.

### 1. **Gleaning Model**
   - **Concept**: The Gleaning model focuses on dynamically gathering and curating information from various sources. It's often used in knowledge management systems where information is constantly being updated and needs to be synthesized regularly.
   - **Example**:
     - **Gleaning Knowledge**: Files related to ongoing research or content creation are automatically pulled together from different locations. For example, articles, PDFs, and notes on "AI Trends" are aggregated into a single dynamic repository that updates as new information is added.
     - **Folder Structure**:
       ```
       /Research
           /AI Trends
               /Article1.pdf
               /Notes_2024.docx
               /Collected Data
       ```


### 3. **Digital Gardening**
   - **Concept**: A concept inspired by the idea of cultivating knowledge like a garden, where ideas are continuously “grown,” pruned, and interlinked. This model is often used in personal knowledge management systems.
   - **Example**:
     - **Digital Garden**: Notes, ideas, and references are maintained in a “garden” where each file is connected to related content. This could be implemented with tools like Roam Research or Obsidian, where each note or file links to others contextually.
     - **Folder Structure**:
       ```
       /Digital Garden
           /Ideas
               /Note1.md
               /Note2.md
           /References
               /Book_Summary_A.pdf
               /Research_Paper_X.pdf
       ```

### 4. **Federated Wiki Model**
   - **Concept**: Inspired by the federated wiki concept, this model allows for decentralized management of files and information, where files are organized in small, interconnected “wikis” or repositories that can be shared across different systems or users.
   - **Example**:
     - **Decentralized Projects**: Files are organized into small, independent repositories that link to other relevant repositories. For instance, a project wiki for "Sustainability Research" that links to another wiki focused on "Green Technology."
     - **Folder Structure**:
       ```
       /Wikis
           /Sustainability Research
               /Introduction.md
               /Energy_Resources.md
           /Green Technology
               /Solar_Power.md
               /Wind_Energy.md
       ```

### 5. **Smart Tagging and Contextual Systems**
   - **Concept**: Instead of traditional folders, this model uses tags and metadata to organize files dynamically. Files can appear in multiple virtual folders or contexts based on their tags.
   - **Example**:
     - **Contextual Tagging**: A file like `Budget_2024.xlsx` might be tagged with "Finance," "2024," and "Budget." It would appear in virtual folders for each tag.
     - **Virtual Folder Structure**:
       ```
       /Finance
           /Budget_2024.xlsx
       /2024
           /Budget_2024.xlsx
       /Budget
           /Budget_2024.xlsx
       ```

### 6. **Knowledge Graphs**
   - **Concept**: Knowledge graphs use nodes and edges to represent files and their relationships, often used in AI systems to manage and retrieve information contextually.
   - **Example**:
     - **Knowledge Representation**: Files like `Climate_Change_Report.pdf` are represented as nodes connected to related nodes such as `Environmental_Policies.docx` and `Renewable_Energy_Strategies.pdf`.
     - **Graph Structure**:
       ```
       /Knowledge Graph
           /Climate_Change_Report.pdf
               /Related Node: Environmental_Policies.docx
               /Related Node: Renewable_Energy_Strategies.pdf
       ```
