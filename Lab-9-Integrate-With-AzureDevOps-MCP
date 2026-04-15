# 🧪 Lab Guide: Connect to Azure Repos using MCP Server in GitHub Copilot & Review Pull Requests

---

## 🎯 Lab Objective

In this lab, you will learn how to:

* Integrate **Azure Repos** with **GitHub Copilot** using **Model Context Protocol (MCP)**
* Configure MCP server for Azure DevOps
* Use Copilot Agent Mode to:

  * Fetch open Pull Requests
  * Analyze PR changes
  * Perform AI-assisted code reviews

---

## 📋 Prerequisites

Ensure you have the following:

* Access to Azure DevOps
* An existing Azure Repos project with active Pull Requests
* GitHub Copilot enabled
* Visual Studio Code installed
* Access to Copilot Chat with **Agent Mode**
* Git installed locally

---

## 🧩 Lab Overview

This lab consists of:

1. Environment Setup
2. MCP Server Configuration for Azure Repos
3. Authentication & Validation
4. Fetching Pull Requests using Copilot
5. Reviewing Pull Requests using AI
6. Advanced Review & Insights

---

# 🚀 Step 1: Environment Setup

## 🛠️ Task 1: Open Project in VS Code

1. Open your local project in **Visual Studio Code**
2. Ensure:

   * Copilot Chat extension is installed
   * You are signed into GitHub
3. Open Copilot Chat panel

---

## 🛠️ Task 2: Enable Agent Mode

1. In Copilot Chat panel
2. Switch to **Agent Mode**

✅ Expected Outcome:

* Copilot can execute external tool actions

---

# 🔌 Step 2: Configure MCP Server for Azure Repos

## 📖 Understanding MCP for Azure

MCP allows Copilot to:

* Communicate with Azure DevOps APIs
* Perform repository operations
* Fetch Pull Requests and metadata

---

## 🛠️ Task 3: Create MCP Configuration File

1. Navigate to project root
2. Create folder (if not exists):

```
.vscode/
```

3. Create file:

```
.vscode/mcp.json
```

---

## 🛠️ Task 4: Add Azure MCP Server Configuration

Paste the following:

```json id="azmcp001"
{
  "inputs": [
    {
      "id": "ado_org",
      "type": "promptString",
      "description": "Azure DevOps organization name  (e.g. 'contoso')"
    }
  ],
  "servers": {
    "ado": {
      "type": "stdio",
      "command": "npx",
      "args": ["-y", "@azure-devops/mcp", "${input:ado_org}"]
    }
  }
}
```

🔁 Replace:

* `{organization}` → Your Azure DevOps organization name

---

## 🛠️ Task 5: Save & Activate MCP Server

1. Open `mcp.json`
2. Click **Start Server**
3. Authenticate when prompted

---

## 🔐 Step 3: Authentication Setup

## 🛠️ Task 6: Authenticate with Azure DevOps

You may be prompted for:

* Azure DevOps login
* Personal Access Token (PAT)

### 🔑 Generate PAT:

1. Go to Azure DevOps → User Settings
2. Select **Personal Access Tokens**
3. Create token with:

   * Code (Read & Write)
   * Pull Request (Read & Write)

---

## 🛠️ Task 7: Verify MCP Tools

1. Open Copilot Chat
2. Click 🛠️ icon

✅ Expected Outcome:

* Azure DevOps tools visible (PRs, repos, etc.)

---

# 🔍 Step 4: Fetch Open Pull Requests

## 🛠️ Task 8: Get All Open PRs

Use prompt:

```plaintext id="fetchpr001"
List all open pull requests in my Azure repository
```

---

## 🛠️ Task 9: Validate Tool Execution

* Copilot will:

  * Call MCP tool
  * Fetch PR data
* Approve the request when prompted

---

## 🛠️ Task 10: Refine Query

```plaintext id="fetchpr002"
List open pull requests with title, author, and status
```

---

✅ Expected Outcome:

* List of open PRs with metadata

---

# 🤖 Step 5: Review Pull Requests using Copilot

## 🛠️ Task 11: Select a PR

Prompt:

```plaintext id="reviewpr001"
Get details of pull request #<PR_ID>
```

---

## 🛠️ Task 12: Analyze Changes

```plaintext id="reviewpr002"
Analyze the code changes in this pull request and summarize them
```

---

## 🛠️ Task 13: Perform Code Review

```plaintext id="reviewpr003"
Review this pull request for:
- Code quality
- Security issues
- Performance concerns
- Best practices
```

---

## 🛠️ Task 14: Suggest Improvements

```plaintext id="reviewpr004"
Suggest improvements and refactored code for this pull request
```

---

## 🛠️ Task 15: Add Review Comments

```plaintext id="reviewpr005"
Add review comments on the pull request highlighting issues and suggestions
```

👉 Approve MCP action

---

✅ Expected Outcome:

* AI-generated review comments added to PR

---

# 🔁 Step 6: Advanced PR Analysis

## 🛠️ Task 16: Compare Multiple PRs

```plaintext id="advpr001"
Compare all open pull requests and identify the most critical one
```

---

## 🛠️ Task 17: Risk Assessment

```plaintext id="advpr002"
Identify high-risk changes across all open pull requests
```

---

## 🛠️ Task 18: Prioritize Reviews

```plaintext id="advpr003"
Prioritize pull requests based on impact and complexity
```

---

# 🔍 Step 7: Best Practices

* Always validate Copilot suggestions before applying
* Review MCP tool permissions carefully
* Avoid automatic approvals in production
* Use smaller prompts for better results
* Combine with project instruction sets

---

# ⚠️ Common Issues & Fixes

| Issue                  | Solution                 |
| ---------------------- | ------------------------ |
| MCP tools not visible  | Restart VS Code          |
| Authentication failure | Regenerate PAT           |
| No PRs returned        | Verify repository access |
| Tool execution denied  | Approve prompt manually  |

---

# 🎉 Lab Completion

You have successfully:

* Connected Azure Repos with MCP
* Enabled Copilot Agent Mode
* Retrieved Pull Requests
* Performed AI-based code reviews
* Automated PR feedback using Copilot

---

# 🧠 Key Takeaways

* MCP enables Copilot to interact with external systems
* Azure DevOps integration enhances DevOps workflows
* Copilot can assist in real-time code reviews
* AI + MCP = Intelligent DevOps automation

---

# 🚀 Bonus Exercises

* Automate PR approval workflow
* Integrate with CI/CD pipelines
* Use Copilot to fix PR issues automatically
* Add multi-repo MCP integration

---

Happy Learning & Reviewing! 🚀
