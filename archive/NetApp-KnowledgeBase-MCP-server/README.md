# NetApp Workload Factory GenAI MCP server

The NetApp BlueXP Workload Factory for GenAI Model Context Protocol (MCP) server enables MCP-based AI agents to interact with Workload Factory for GenAI knowledge bases.

To learn more about NetApp BlueXP, visit the [BlueXP documentation](https://docs.netapp.com/us-en/bluexp-setup-admin/concept-overview.html).

For more information about NetApp BlueXP identity and access management, you can read the [BlueXP identity and access management overview](https://docs.netapp.com/us-en/bluexp-automation/tenancyv4/overview.html).

## NetApp Workload Factory GenAI MCP server requirements

- You need [Node.js](https://nodejs.org/) 23 or later (stable version).
- You need a tenancy account in NetApp BlueXP.
- You need a service account created in your BlueXP tenancy account.
    - You can create a service account from the **Identity & access management** area in the BlueXP console.
- You need to note the following from the service account:
    - Account ID
    - Client ID (available in the **Service account credentials** area in the BlueXP console)
    - Client Secret (available in the **Service account credentials** area in the BlueXP console)
- The GenAI knowledge base name must be 53 characters or less in length.
- You need to note the description of the GenAI knowledge base. This description will be used by the MCP client to access the GenAI knowledge base with the MCP server.

## Register the MCP server as a BlueXP service
You need to register the MCP server as a BlueXP service before you configure and install the MCP server.

Register the MCP server as a BlueXP service.

1. Navigate to the BlueXP website using a browser: https://console.bluexp.netapp.com
2. Sign in using your NetApp Cloud credentials or your NetApp Support Site credentials.
3. Select the **Account** tab at the top of the web UI.
4. Select **Manage Account** and select the Members tab.
5. Select **Create Service Account** and provide the details for the service account.
6. Select **Create** to register the application. After the application is registered, the client ID and client secret of the service are displayed.
7. Copy or download the client ID and client secret. The client secret is visible only once and is not stored anywhere by BlueXP. Copy or download the secret and store it safely.

For further information, refer to the [BlueXP documentation](https://docs.netapp.com/us-en/bluexp-automation/platform/register_service.html).

## Configure the MCP server
After configuring service details for BlueXP, you're ready to configure the MCP server. Update the following variables in the MCP server `config/config.env` file with values from your environment:
```
ACCOUNT_ID=<service_account_ID>
CLIENT_ID=<service_account_client_ID>
CLIENT_SECRET=<service_account_client_secret>
```

## Install the server
To install the MCP server, run the following command:

```bash
npm install
```

## Build the server
To build the MCP server, run the following command:

```bash
npm run build
```

## Configure the Claude Desktop client to connect to the server
As an example, you can configure Claude Desktop to connect to the GenAI MCP server using the MCP server Desktop Extension.

1. In BlueXP Identity & access management, view and save the tenant account ID and credentials of the service account that can access GenAI knowledge bases.
2. [Download](https://github.com/NetApp/mcp/tree/main/NetApp-KnowledgeBase-MCP-server) the GenAI MCP server .dxt file.
3. In Claude Desktop, go to **File > Settings > Extensions**.
4. Drag the .dxt file you downloaded onto the settings window. The extension's description appears.
5. Select **Install**.
6. Paste the BlueXP tenant account ID and service account credentials into the fields that appear, and select **Save**.
7. Toggle the **Disabled** switch near the top of the window to **Enabled**.
8. Close the settings dialog.

## Configure Amazon Q Developer to connect to the server
Follow these steps to configure Amazon Q developer for CLI or IDE to connect to the GenAI MCP server.

1. Ensure that Amazon Q Developer is running on your workstation.
2. Edit the configuration JSON file (located at `~/.aws/amazonq/mcp.json` on Linux or Mac systems) and use the following example JSON configuration, replacing content in brackets <> with the path to the GenAI MCP server package:
    ```json
    {
      "mcpServers": {
        "workload-factory-gen-ai": {
          "command": "node",

          "args": [
            "--env-file=<path_to_the_mcp_server_package>/config/config.env",
            "<path_to_the_mcp_server_package>/build/index.js"
          ]
        }
      }
    }
    ```
3. Save the file.
4. Test the configuration and chat capabilities using the following Amazon Q developer CLI commands:
    ```
    q mcp list
    q chat
    ```

## Learn More

Learn more about [BlueXP Workload Factory for GenAI](https://docs.netapp.com/us-en/workload-genai/index.html).
