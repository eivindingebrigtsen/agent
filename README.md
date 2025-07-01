# AI-Powered Gitflow with n8n

This project contains a set of n8n workflows designed to automate a complete Gitflow process using AI agents.

## Prerequisites

1.  **A running n8n instance:** This can be a cloud-hosted or self-hosted instance.
2.  **GitHub Account:** With a repository created. This has already been done and is located at [https://github.com/eivindingebrigtsen/agent](https://github.com/eivindingebrigtsen/agent).
3.  **AI Provider Account:** An account with an AI provider like Google (for Gemini) or OpenAI.

## Setup Instructions

### 1. Create Credentials in n8n

Before importing the workflows, you need to set up the necessary credentials in your n8n instance.

*   **GitHub:**
    1.  In n8n, go to **Credentials** > **Add credential**.
    2.  Search for `GitHub API` and select it.
    3.  Follow the on-screen instructions to connect your GitHub account.
    4.  Note the **ID** of the created credential (you can see it in the URL or by reopening the credential).

*   **AI Provider (Gemini Example):**
    1.  In n8n, go to **Credentials** > **Add credential**.
    2.  Search for `Google Gemini API` and select it.
    3.  Follow the on-screen instructions to add your API key.
    4.  Note the **ID** of the created credential.

### 2. Import and Configure Workflows

You need to import the 5 JSON files from the `.n8n` directory into your n8n instance.

For each workflow:

1.  Go to your n8n dashboard and click **Add workflow**.
2.  Select **Import from file** and choose one of the `.json` files.
3.  **Configure Credentials:**
    *   Find the nodes that require credentials (e.g., `GitHub: Create Issue`, `AI Agent: ...`).
    *   In the node settings, you'll see a `Credential` field.
    *   Replace the placeholder ID (`YOUR_GITHUB_API_CREDENTIAL_ID` or `YOUR_GEMINI_API_CREDENTIAL_ID`) with the actual ID you noted in the previous step.
4.  **Activate the Workflow:** By default, imported workflows are inactive. Click the **Active** toggle at the top of the screen to enable it.

### 3. Set Up GitHub Webhooks

Workflows 2, 3, 4, and 5 are triggered by events in your GitHub repository.

For each of these workflows:

1.  Open the workflow in the n8n editor.
2.  Click on the `GitHub Trigger` node.
3.  You will see a **Webhook URL**. Copy this URL.
4.  In your GitHub repository (`eivindingebrigtsen/agent`), go to **Settings** > **Webhooks**.
5.  Click **Add webhook**.
6.  Paste the URL from n8n into the **Payload URL** field.
7.  For the **Content type**, select `application/json`.
8.  Under **Which events would you like to trigger this webhook?**, select **Let me select individual events.**
9.  Uncheck `Pushes` and select the specific events required by the trigger node (e.g., for Workflow 2, select `Issues`).
10. Click **Add webhook**.

Repeat this for all workflows that have a `GitHub Trigger` node.

## Running the Workflow

Once everything is set up, you can start the process by running the first workflow.

1.  **Open "Gitflow: 1 - Task Intake & Issue Creation" in n8n.**
2.  Click **Test workflow** in the top-right corner.
3.  In the `Start` node's test window, enter a task description in the `task_description` field. For example: `Create a README.md file with setup instructions`.
4.  Click **Execute**.

This will trigger the first agent, which will create a GitHub issue. The creation of that issue will then trigger the second workflow, and so on, through the entire automated process.
