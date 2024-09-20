# Simple To-Do List with Node-RED and IBM Cloudant

This project creates a simple to-do list application using Node-RED and IBM Cloudant. The application allows users to add tasks via a form, store them in a Cloudant database, and display the tasks on a dashboard.

## Components

- **Node-RED**: For building the flow.
- **IBM Cloudant**: To store the tasks.
- **IBM Cloud (Optional)**: Hosting Node-RED and the dashboard.

## Prerequisites

- IBM Cloud account
- Node-RED installed locally or deployed on IBM Cloud
- Cloudant service instance

## Setup Instructions

### 1. Set Up Node-RED

- Install Node-RED locally or deploy it on IBM Cloud using the Node-RED Starter Kit.

#### 1. **HTTP In Node**
- **Purpose**: This node listens for incoming HTTP requests.
- **Configuration**: 
  - **URL**: `/add-task`
  - **Method**: `POST`
- **Function**: It triggers the flow when a POST request is made to the `/add-task` endpoint.

#### 2. **Function Node**
- **Purpose**: This node processes and formats the incoming data.
- **Configuration**: 
  - **Function Code**:
    ```javascript
    msg.payload = {
        task: msg.payload.task,
        status: "pending",
        created_at: new Date().toISOString()
    };
    return msg;
    ```
- **Function**: It takes the task data from the HTTP request, adds a status and timestamp, and prepares it for storage in Cloudant.

#### 3. **Cloudant Out Node**
- **Purpose**: This node inserts data into the Cloudant database.
- **Configuration**: 
  - **Service**: Your Cloudant service instance.
  - **Database**: `mydb`
  - **Operation**: `insert`
- **Function**: It stores the formatted task data in the specified Cloudant database.

#### 4. **UI Form Node**
- **Purpose**: This node creates a form in the Node-RED dashboard for adding tasks.
- **Configuration**: 
  - **Label**: `Add Task`
  - **Group**: `TASK`
  - **Fields**: 
    - **Task**: Text input for the task description.
    - **Description**: Optional text input for additional details.
- **Function**: It provides a user interface for entering new tasks.

#### 5. **UI Group Node**
- **Purpose**: This node defines a group in the Node-RED dashboard.
- **Configuration**: 
  - **Name**: `TASK`
  - **Tab**: `TASK LIST`
  - **Width**: `6`
- **Function**: It organizes the UI elements into a group on the dashboard.

#### 6. **UI Tab Node**
- **Purpose**: This node defines a tab in the Node-RED dashboard.
- **Configuration**: 
  - **Name**: `TASK LIST`
  - **Icon**: `dashboard`
- **Function**: It creates a tab in the dashboard where the task list and form will be displayed.

#### 7. **Cloudant Configuration Node**
- **Purpose**: This node holds the configuration for connecting to your Cloudant service.
- **Configuration**: 
  - **Host**: Your Cloudant service URL.
- **Function**: It provides the necessary credentials and connection details for the Cloudant nodes to interact with the database.

These nodes work together to create a flow that allows users to add tasks via a form, store them in a Cloudant database, and display them on a dashboard.


### 3. Configure the Nodes

- **HTTP In Node**: Set the URL to `/add-task` and method to `POST`.
- **Function Node**: Format the task data.
- **Cloudant Out Node**: Configure to insert data into your Cloudant database.
- **UI Form Node**: Create a form for adding tasks.
- **UI Table Node**: Display the tasks on the dashboard.

### 4. Create IAM Credentials in IBM Cloud

To create IAM credentials for your Cloudant service, follow these steps:

1. **Log in** to your IBM Cloud account.
2. **Navigate** to the **Resource List** from the IBM Cloud console.
3. **Select** your Cloudant service instance.
4. Click on **Service credentials**.
5. Click **New Credential+**.
6. Provide a **Name** for the credential.
7. Specify the **Role** (e.g., `Manager`).
8. Optionally, provide a **Service ID** or let IAM generate one for you.
9. Click **Add** to generate the new service credential¹.

### 5. Deploy the Flow

- Click the **Deploy** button in Node-RED to activate your flow.

### 6. Test the Flow

- Open the Node-RED dashboard.
- Add tasks using the form.
- Verify that tasks are stored in Cloudant and displayed on the dashboard.

## Optional: Deploy on IBM Cloud

- Follow the steps to deploy your Node-RED application on IBM Cloud using the Node-RED Starter Kit.

## Contact

For any questions or support, please contact [Keerthi](mailto:keerthi.ece.software@gmail.com).

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
