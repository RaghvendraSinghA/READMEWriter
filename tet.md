## AMA Q&A

### What is the `CLAUDE.md` file in Claude? (Aditya Sharma)

- CLAUDE.md is a Markdown file used by Claude Code to store project-specific instructions and context.     
- Claude Code can read it to understand the project structure, coding conventions, testing commands, and development guidelines.    
- We can also store re-occuring tasks outputs in this file to save time and computation.
- Claude.md is loaded each time, session starts.


### What is the agent loop? (Alok Kumar)

The agent loop is the repeated process through which an AI agent understands a task, takes actions,     
observes results, and decides what to do next.

It starts after user gives prompt and ends after satisfying result.

User gives prompt --> AI gathers context --> take action --> verify result (If result not upto the standards then again start   
from gather context and come to verify result untill output is satisfactory ---> End (When output is accurate). 


### What do Explore, Code, and Commit mean? (Amit Chandra Dey)

Explore, Code, and Commit describe a useful workflow for AI-assisted software development.

**1. Explore**

Understand the codebase before making changes.

Activities include:
- Reading relevant source files.
- Understanding project structure.
- Identifying dependencies.

**2. Code**

Implement the required functionality or fix.

Activities include:
- Editing source files.
- Adding functions or features.

Example:

**3. Commit**

Review the changes and save them in version control when they are ready.



### What is the 4D framework? (Atul Kumar)

The term **4D framework** can refer to different frameworks depending on the course or context.
One commonly used AI collaboration interpretation is:

- **Delegation:** Decide which tasks are suitable for AI assistance. Deligate task according to AI's capabilities.
- **Description:** Explain the task, context, constraints, role, and expected outcome etc.
- **Discernment:** Evaluate the AI's output critically for accuracy, quality, and safety and use agentic loop if output not accurate.     
- **Diligence:** Be transparent about using AI to complete the task and take responsibilities of your actions,    
                like puhsing AI generated code to codebase, or creating company financial report using AI and submitting to      
                company.


### What is a terminal? (Pantham Adinarayana)

A **terminal** is a text-based interface that allows you to interact with your computer by entering commands.

Developers use terminals to:
- Navigate directories.
- Create and manage files.
- Install dependencies.

**Example commands on macOS or Linux:**

```bash
# Display the current directory
pwd

# List files and directories
ls

```


### What is context management? (Sibsankar Manna)

**Context management** is the process of selecting, organizing, and maintaining the 
information an AI model needs to complete a task effectively.

Context can include:
- User instructions and conversation history.
- System instructions.
- Project guidance from `CLAUDE.md`.
- Relevant source code and documentation.

A model has a limited context window, so providing relevant information is important.
Too much unrelated information can make a task less efficient and harder to reason about.


Good context management may involve:
- Keeping `CLAUDE.md` clear and relevant.
- Reading only the files needed for the task.
- Providing useful error messages and logs.
- Summarizing important findings during long tasks.

- Use subagents to delegate asks and let them handle the task parallelly in their own context which will not pollute and take memory    
space of main agent context.
- Use /compact command to make space but /compact may remove important information.

