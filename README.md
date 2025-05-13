# Azure AI Foundry Chat Client

This project demonstrates how to use Azure AI services to build a chat client that interacts with an AI model to provide intelligent responses to user prompts.

## Table of Contents

- [Prerequisites](#prerequisites)
- [Setup](#setup)
- [Running the Code](#running-the-code)
- [Environment Variables](#environment-variables)
- [Project Structure](#project-structure)
- [Troubleshooting](#troubleshooting)

---

## Prerequisites

Before running this project, ensure you have the following installed:

1. **Python 3.10 or higher**: The project requires Python 3.10 or later.
2. **Azure Account**: An active Azure subscription is required to use Azure AI services.
3. **Azure AI Resources**:
   - Azure AI Project with a deployed model.
   - Connection string for the Azure AI Project.
4. **Virtual Environment**: It is recommended to use a virtual environment to manage dependencies.

---

## Setup

Follow these steps to set up the project:

1. **Clone the Repository**:

   ```bash
   git clone <repository-url>
   cd AZURE_AI_FOUNDRY
   ```

2. **Create a Virtual Environment**:

   ```bash
   python3 -m venv Azure
   source Azure/bin/activate  # For Linux/Mac
   Azure\Scripts\activate     # For Windows
   ```

3. **Install Dependencies**:

   Install the required Python packages using `pip`:

   ```bash
   pip install -r requirements.txt
   ```

   If `requirements.txt` is not available, manually install the dependencies:

   ```bash
   pip install azure-identity azure-ai-projects python-dotenv
   ```

4. **Set Up Environment Variables**:

   Create a `.env` file in the `PROJECT` directory with the following content:

   ```env
   PROJECT_CONNECTION=<your_project_connection_string>
   MODEL_DEPLOYMENT=<your_model_name>
   ```

   Replace `<your_project_connection_string>` and `<your_model_name>` with your Azure AI Project connection string and model name, respectively.

---

## Running the Code

To run the chat client, navigate to the appropriate directory and execute the script:

1. **Run the Chat Client**:

   ```bash
   python LEARN_FOLDER/chat_client.py
   ```

2. **Provide Input**:

   When prompted, enter a question or prompt for the AI assistant. Type `quit` to exit the program.

---

## Environment Variables

The project relies on the following environment variables:

- `PROJECT_CONNECTION`: The connection string for your Azure AI Project.
- `MODEL_DEPLOYMENT`: The name of the deployed model to use for chat completions.

These variables can be set in a `.env` file or directly in your environment.

---

## Project Structure

The project is organized as follows:

```plaintext
AZURE_AI_FOUNDRY/
├── Azure/                  # Virtual environment folder
├── LEARN_FOLDER/           # Learning and experimentation scripts
│   ├── chat_client.py      # Main chat client script
│   ├── client_app.py       # Additional client application
│   ├── Primary.py          # Primary script for other tasks
├── PROJECT/                # Main project folder
│   ├── .env                # Environment variables file
│   ├── chat-app.py         # Main application script
├── README.md               # Project documentation
├── LICENSE                 # License information
└── requirements.txt        # Python dependencies
```

---

## Troubleshooting

1. **Missing Dependencies**:

   If you encounter missing dependencies, ensure you have installed all required packages using `pip install -r requirements.txt`.

2. **Azure Authentication**:

   Ensure you are authenticated with Azure. Use the `az login` command if necessary.

3. **Environment Variables Not Loaded**:

   If environment variables are not loaded, double-check the `.env` file and ensure it is in the correct directory.

4. **Connection Issues**:

   Verify that the `PROJECT_CONNECTION` string is correct and that your Azure AI Project is active.

---

## License

This project is licensed under the Apache License 2.0. See the `LICENSE` file for details.
