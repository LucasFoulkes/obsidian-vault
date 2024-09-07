To transform the document into a more effective technical diary, we'll retain the detailed and reflective elements that are crucial for this format. A technical diary should document not only the steps and processes but also the thoughts, challenges, solutions, and decisions made along the way. Here's an improved version with added structure and clarity.

---

# Financial Tracking System Technical Diary

## Project Overview
### Goal
- **Objective:** Develop a system to accurately track and analyze all financial transactions, including revenue, expected earnings, and actual deposits, integrating data from various sources into a consolidated tracker.

### Purpose of this Diary
- This diary is a comprehensive record of the journey to build the financial tracking system. It captures every step, challenge, decision, and reflection, ensuring a detailed account of the process is maintained for future reference.

---

## Daily Log

### 14/08/2024

#### Data Collection - WhatsApp Conversations

**Objective:** Extract financial data from relevant WhatsApp group chats.

- **Current Status:** Reviewed chat logs from the group "Reto X Milenium Plaza" for the period from 14/05/2024 to 14/08/2024. Noticed that there are significant gaps in the data, likely due to disappearing messages or potentially deleted conversations.
  
  **Reflection:** The gaps are concerning as they could significantly impact the accuracy of the financial tracking system. I need to explore alternative ways to recover this missing data. My options include reaching out to group members to see if they have backups or using other devices that might have retained the chat history.

- **Challenges:** Unable to retrieve older conversations from "Lukasvr" chat covering 12/11/2023 to 25/06/2023. Data appears to be missing, and I suspect disappearing messages were activated.

  **Next Steps:**
  1. Investigate if any group members have the missing conversations stored on their devices.
  2. Research possible recovery methods for disappearing WhatsApp messages, although preliminary online searches suggest this might be futile.
  3. Consider the possibility of leveraging data from the VR machine itself to fill in the gaps.

#### Data Collection - VR Machine Logs

**Objective:** Retrieve financial logs directly from the VR machine to cross-verify with WhatsApp data.

- **Current Status:** Successfully connected to the VR machine via TeamViewer, though I struggled with password recall issues. I found a file named `tmpemails.xlsx` in the VR folder, which might contain relevant data, but it’s in a zipped format and requires further investigation.
  
  **Reflection:** The discovery of this file is promising, though the password issue is frustrating. I might need to consider using password recovery tools or contacting someone who might remember it. Also, there’s a lingering worry about whether the system reinstallation might have wiped critical data.

- **Challenges:** Potential loss of data due to system reinstallation. The historical data might not be complete, especially if employees recorded errors or misentered player counts.

  **Next Steps:**
  1. Unzip and examine the contents of `tmpemails.xlsx`.
  2. Cross-check this data with whatever is available from the WhatsApp conversations.
  3. Explore if SSH or another remote access method could provide easier access in the future.
  4. Set up a more reliable backup system to prevent data loss going forward.

---

### 15/08/2024

#### Data Structuring

**Objective:** Organize all collected data into a standardized format for easier analysis.

- **Current Status:** Defined a schema for the data, focusing on key fields: Datetime, Employee, Ride, Revenue, Costs, Deposits. Started parsing the WhatsApp data, but progress is slow due to the missing messages.
  
  **Reflection:** The normalization process is crucial, but it’s clear that without complete data, the insights gained will be limited. I need to find a way to reconcile or estimate missing data points without compromising accuracy.

- **Challenges:** The schema seems appropriate, but there’s uncertainty about how to handle incomplete data. Considering adding a "Data Source" field to track where each piece of information came from, which might help in identifying patterns in missing data.

  **Next Steps:**
  1. Continue parsing the available data.
  2. Develop a method for estimating missing data points, possibly by using averages from known data.
  3. Review the schema periodically to ensure it remains aligned with the evolving needs of the analysis.

---

### 16/08/2024

#### Data Analysis and Insights

**Objective:** Begin analyzing the structured data to identify key financial insights.

- **Current Status:** Started with a preliminary analysis focusing on the impact of price changes (e.g., Juliana’s charges) on sales. Early indications suggest a potential drop in sales corresponding with the price increase, but the incomplete data makes it difficult to draw firm conclusions.
  
  **Reflection:** The analysis is revealing some trends, but I’m hesitant to make any definitive claims without a more complete dataset. It’s becoming clear that I’ll need to make some educated guesses or use statistical methods to fill in gaps.

- **Challenges:** The incomplete data continues to be a significant hurdle. I’m considering the use of predictive modeling or machine learning to estimate missing values, though this adds complexity to the project.

  **Next Steps:**
  1. Deepen the analysis once more data is available.
  2. Explore simple statistical models for estimating missing data.
  3. Document all assumptions made during the analysis to maintain transparency.

---

### 17/08/2024

#### System Development

**Objective:** Create a comprehensive system for ongoing financial tracking and analysis.

- **Current Status:** Outlined the basic structure of the system. It will need to handle inputs for all payments and costs, automatically reconcile discrepancies, and generate reports. Currently exploring software options or custom development.

  **Reflection:** The system is the heart of this project, and it needs to be robust and user-friendly. I’m leaning towards a custom solution that could be tailored to the specific needs identified so far, but this will require more time and potentially bringing in external help.

- **Challenges:** Deciding between off-the-shelf software and custom development. The latter offers flexibility but requires more resources.

  **Next Steps:**
  1. Evaluate software options for financial tracking.
  2. If opting for custom development, outline key features and begin prototyping.
  3. Set up a trial with real data to test the system’s effectiveness.

---
