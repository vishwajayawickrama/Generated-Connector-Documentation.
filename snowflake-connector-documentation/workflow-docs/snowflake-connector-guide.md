# Snowflake Connector Example

## What You'll Build

In this guide, you will build a Ballerina integration using the WSO2 Integrator: BI low-code canvas that connects to a Snowflake data warehouse and executes an SQL INSERT statement. The integration uses the **Automation** entry point pattern, which runs as a standalone program without requiring an HTTP listener.

- **Connector:** `ballerinax/snowflake:2.2.0`
- **Integration pattern:** Automation (scheduled/manual trigger)
- **Operations used:**
  - `snowflake:Client->execute` — Executes a parameterized SQL statement against a Snowflake database and returns an `sql:ExecutionResult`

---

## Prerequisites

- WSO2 Integrator: BI extension installed in VS Code (code-server at `http://localhost:8080`)
- Ballerina Swan Lake Update 13 (version 2201.13.1) installed
- A Snowflake account with the following details available:
  - Account Identifier (e.g., `myorg-myaccount`)
  - Username and Password with sufficient privileges
  - An existing Warehouse, Database, Schema, and Role
- The `~/bi-workspace` folder available as the workspace root

---

## Setting Up the Snowflake Integration

### Step 1 — Open the workspace in VS Code

Launch code-server and open the `~/bi-workspace` folder. The WSO2 Integrator: BI panel appears in the Primary Side Bar once the extension activates.

![VS Code clean workspace with bi-workspace folder open](../screenshots/snowflake_step_01_vscode_clean.png)

### Step 2 — Open the WSO2 Integrator: BI panel

Click the WSO2 Integrator: BI icon in the Activity Bar (left side bar) to open the BI panel. The panel shows the **Create New Integration** button at the top.

![WSO2 Integrator BI panel open in the side bar](../screenshots/snowflake_step_02_bi_panel.png)

### Step 3 — Create a new integration project

Click **Create New Integration**, enter `snowflake-db-connection` as the project name, select the `~/bi-workspace` directory as the location, and confirm. The low-code canvas opens automatically, showing a blank design surface with the Artifacts panel on the left.

![New integration canvas for snowflake-db-connection project](../screenshots/snowflake_step_03_new_integration_canvas.png)

---

## Adding the Snowflake Connector

### Step 4 — Open the Component Palette

In the low-code canvas, click the **+** (Add Component) button or select **Add Connection** from the Artifacts panel to open the Component Palette. The palette displays a search box and a list of available connectors from Ballerina Central.

![Component palette open showing connector search](../screenshots/snowflake_step_04_component_palette.png)

### Step 5 — Search for the Snowflake connector

Type `snowflake` in the search box. The palette filters the results and displays the `ballerinax/snowflake` connector card published on Ballerina Central.

![Snowflake connector appearing in search results](../screenshots/snowflake_step_05_connector_search_results.png)

### Step 6 — Add the connector to the canvas

Click the `ballerinax/snowflake` connector card. The **Configure Snowflake Connection** panel slides open on the right side of the canvas.

![Configure Snowflake Connection panel open after selecting connector](../screenshots/snowflake_step_06_connector_added_to_canvas.png)

---

## Configuring the Snowflake Connection

### Step 7 — Fill in the connection parameters

Complete all required fields in the Configure Snowflake Connection panel using the values below:

- **Account Identifier:** `myorg-myaccount`
- **Username:** `SNOWFLAKE_USER`
- **Password:** `<your-snowflake-password>`
- **Options (Advanced Configurations):** Click the **Options** field to open the Record Configuration helper, then enter the following expression in the code editor:
  ```
  {properties: {"db": "TEST_DB", "schema": "PUBLIC", "warehouse": "COMPUTE_WH", "role": "SYSADMIN"}}
  ```
  Click **Save** in the Record Configuration panel to apply the value.
- **Connection Name:** `snowflakeConnection`

![Connection form with all parameters filled in](../screenshots/snowflake_step_07_connection_form_filled.png)

### Step 8 — Save the connection

Click the **Save** button at the bottom of the Configure Snowflake Connection panel. The connection is validated and persisted to `connections.bal`. The canvas refreshes to display the `snowflakeConnection` node in the **Connections** section of the Artifacts panel.

![Connection saved and appearing on the canvas](../screenshots/snowflake_step_08_connection_saved.png)

### Step 9 — Verify the connection in the sidebar

The left-side Artifacts tree now lists `snowflakeConnection` under **Connections**. This confirms the `ballerinax/snowflake:2.2.0` module was pulled from Ballerina Central and the client was successfully initialized.

![snowflakeConnection listed in the Artifacts sidebar](../screenshots/snowflake_step_09_connection_in_sidebar.png)

---

## Configuring the Snowflake Execute Operation

### Step 10 — Create an Automation entry point

Click **+** next to **Entry Points** in the Artifacts panel and select **Automation**. The low-code canvas switches to the Automation flow diagram, which shows a **Start** node connected to an **End** node. The `snowflakeConnection` appears in the available Connections list within the flow editor.

![Automation canvas open with Start node visible](../screenshots/snowflake_step_10_connection_operations_expanded.png)

### Step 11 — Add the Execute operation

Click the **+** button between the Start and End nodes on the Automation canvas to open the statement selector. Navigate to **Connections → snowflakeConnection** and expand it. Select **execute** from the list of available operations. The **Execute Operation** configuration panel opens on the right.

![Execute operation configuration panel open](../screenshots/snowflake_step_11_operation_panel_open.png)

### Step 12 — Fill in the operation parameters

Configure the Execute operation with the following values:

- **sqlQuery:** `` `INSERT INTO test_table (id, name, created_at) VALUES (1, 'test-record', CURRENT_TIMESTAMP())` ``
- **Result Variable Name:** `result`
- **Result Type:** `sql:ExecutionResult`

Click **Save** to confirm the operation configuration.

![Execute operation panel with SQL query and result variable filled in](../screenshots/snowflake_step_12_operation_params_filled.png)

### Step 13 — Verify the Execute node on the canvas

The Automation flow diagram now shows the `snowflake : execute` node inserted between the Start and End nodes. An Error Handler branch is automatically added. The flow reads: **Start → snowflake : execute (result) → Error Handler → End**.

![Execute node visible in the Automation flow canvas](../screenshots/snowflake_step_13_remote_function_on_canvas.png)

---

## Verifying the Snowflake Integration

### Step 14 — Review the complete integration overview

Navigate back to the integration **Overview** canvas (click **Overview** in the breadcrumb or the Artifacts panel header). The design surface displays both artifacts created during this guide:

- **snowflakeConnection** — Connection artifact (Connections section)
- **Automation** — Entry Point artifact (Entry Points section)

The integration is complete. The `snowflakeConnection` client is initialized with the Snowflake account credentials and advanced options, and the Automation entry point executes an INSERT statement into `test_table` on each run.

![Complete integration overview showing connection and automation artifacts](../screenshots/snowflake_step_14_complete_flow_canvas.png)
