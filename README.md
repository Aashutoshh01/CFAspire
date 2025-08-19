# CFAspire 🧠

CFAspire is an intelligent chatbot designed to help users study for the CFA Level 1 exam. It leverages a Retrieval-Augmented Generation (RAG) architecture, powered by Amazon Web Services (AWS) Bedrock, to provide accurate and context-aware answers based on the comprehensive Schweser Notes PDF.

The application uses LangChain to orchestrate the RAG pipeline, Amazon Titan for generating embeddings, Meta's Llama 3 for response generation, and FAISS for efficient vector storage. The entire experience is wrapped in a user-friendly web interface built with Streamlit.

---
## ✨ Key Features

* **AWS Bedrock Integration:** Utilizes powerful foundation models like Meta's Llama 3 and Amazon Titan for embeddings, all managed through AWS.
* **Retrieval-Augmented Generation (RAG):** Provides answers grounded in the provided CFA study material, reducing hallucinations and increasing accuracy.
* **High-Quality Study Source:** Uses the trusted Schweser Notes for the CFA Level 1 exam as its knowledge base.
* **Efficient Vector Storage:** Employs FAISS to create a local vector store for fast and efficient similarity searches.
* **Interactive UI:** A simple and intuitive web interface built with Streamlit allows users to easily create the vector store and ask questions.
* **Modular Code:** Built with LangChain for a clean and maintainable RAG pipeline implementation.

---
## 🎬 Demo

See a live demo of CFAspire in action, from creating the vector store to asking complex finance questions. Click the image below to watch the video.

[![CFAspire Demo Video](https://drive.google.com/uc?export=view&id=1Pthp_VeQIrMeech-ovnRe4fb80KEqcto)](https://drive.google.com/file/d/1ZSAlBrwZkSBY0XJyicMwxWw3744l_ytZ/view?usp=sharing)

---
## 🛠️ Getting Started

Follow these instructions carefully to set up the AWS environment and run the project locally.

### 1. AWS Bedrock and IAM Configuration

This project requires access to foundation models on AWS Bedrock.

#### Step 1: Request Model Access in AWS Bedrock
1.  Log in to your AWS Management Console.
2.  Navigate to the **Amazon Bedrock** service.
3.  In the bottom left corner, click on **Model access**.
4.  Click the **Manage model access** button in the top right.
5.  Request access for the following models:
    * **Titan Embeddings G1 - Text** (`amazon.titan-embed-text-v2:0`)
    * **Llama 3 70b Instruct** (`meta.llama3-70b-instruct-v1:0`)
6.  Wait for the access status to change to "Access granted".

#### Step 2: Create an IAM User with Bedrock Permissions
1.  Navigate to the **IAM (Identity and Access Management)** service in the AWS Console.
2.  Go to **Users** and click **Create user**.
3.  Enter a **User name** (e.g., `cfaspire-user`) and click **Next**.
4.  In "Permissions options," select **Attach policies directly**.
5.  In the "Permissions policies" search bar, type `AmazonBedrockFullAccess` and check the box next to it.
6.  Click **Next**, review the details, and click **Create user**.

#### Step 3: Create an Access Key
1.  Click on the newly created user from the IAM user list.
2.  Go to the **Security credentials** tab.
3.  Scroll down to **Access keys** and click **Create access key**.
4.  For the use case, select **Command Line Interface (CLI)**.
5.  Acknowledge the recommendation and click **Next**.
6.  Click **Create access key**.
7.  **IMPORTANT:** Copy the **Access key** and **Secret access key** and save them somewhere secure. You will not be able to see the secret key again.

#### Step 4: Configure AWS CLI
1.  [Install the AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html) on your local machine if you haven't already.
2.  Open your terminal or command prompt and run the command:
    ```bash
    aws configure
    ```
3.  You will be prompted to enter your credentials. Paste the values you saved in the previous step.
    * **AWS Access Key ID:** `[PASTE YOUR ACCESS KEY HERE]`
    * **AWS Secret Access Key:** `[PASTE YOUR SECRET ACCESS KEY HERE]`
    * **Default region name:** `ap-south-1` (or your preferred region where you enabled model access)
    * **Default output format:** `json`

Your AWS environment is now configured to run the application.

### 2. Local Project Setup

#### Step 1: Clone the Repository
```bash
git clone [https://github.com/YOUR_GITHUB_USERNAME/CFAspire.git](https://github.com/YOUR_GITHUB_USERNAME/CFAspire.git)
cd CFAspire
```
**Note:** Remember to replace `YOUR_GITHUB_USERNAME` with your actual GitHub username.

#### Step 2: Create and Activate Conda Environment
This project uses Python 3.8.
```bash
conda create -n cfaspire python=3.8 -y
conda activate cfaspire
```

#### Step 3: Install Dependencies
```bash
pip install -r requirements.txt
```

---
## 🚀 Usage

The application is run using Streamlit.

1.  Make sure you are in the root directory of the project.
2.  Run the following command in your terminal:
    ```bash
    streamlit run main.py
    ```
3.  Your web browser will open with the application running at **http://localhost:8501**.

### How to Use the App
The application has a two-step process:

1.  **Create the Vector Store:** In the sidebar, click the **"Store Vector"** button. This will read the CFA PDF, split it into chunks, generate embeddings using Amazon Titan, and save them into a local FAISS vector index. This only needs to be done once.
2.  **Ask a Question:** Once the vector store is created, type your question into the main text input box and click the **"Send"** button in the sidebar. The application will retrieve relevant context and generate an answer using Llama 3.

---
## 📂 Project Structure
```
CFAspire/
├── pdf-data/
│   └── CFA_Level_1_Schweser_notes.pdf
├── faiss_index/
│   └── ... (created after running the app)
├── main.py
└── requirements.txt
