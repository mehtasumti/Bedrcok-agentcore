# End-to-end Customer Support Agent with AgentCore

In this tutorial we will move a customer support agent from prototype to production using Amazon Bedrock AgentCore services.

## What You'll Build

A complete customer support system that starts as a simple prototype and evolves into a scalable and secure sample application. 

Your final system will handle real customer conversations with memory, shared tools, and a web interface.

> [!IMPORTANT]
> The examples provided here is for educational purposes. It demonstrates how the different services from AgentCore are used on the process of migrating an agentic use case from prototype to production. As such, it is not intended for direct use in production environments.

**Journey Overview:**
- Start with a basic agent prototype (20 mins)
- Add conversation memory across sessions (20 mins) 
- Share tools securely across multiple agents (30 mins)
- Deploy to production with monitoring (30 mins)
- Build a customer-facing web app (20 mins)

## Architecture Overview

By the end of the 5 labs of this tutorial you will have created the following architecture

<div style="text-align:left">
    <img src="images/architecture_lab5_streamlit.png" width="100%"/>
</div>

## Prerequisites

- AWS account with Bedrock access
- Python 3.10+
- AWS CLI configured
- Claude 3.7 Sonnet enabled in Bedrock
- SageMaker AI Domain (setup instructions below)

## Initial Setup

### 1. Create SageMaker AI Domain

Before starting the labs, you need to set up a SageMaker AI Domain in AWS:

1. **Navigate to Amazon SageMaker** in the AWS Console
2. **Create a Domain** (if you don't already have one)
   - Follow the AWS Console prompts to create a new SageMaker Domain
   - Choose the setup type that fits your needs (Quick setup or Standard setup)

### 2. Configure IAM Role Permissions

After creating your SageMaker Domain, you need to configure the IAM role with appropriate permissions:

#### Add Administrator Access Policy

1. Go to **IAM Console** → **Roles**
2. Find the role attached to your SageMaker Domain
3. Click on **Attach policies**
4. Search for and attach **AdministratorAccess** policy

> **Note:** For production environments, follow the principle of least privilege and create custom policies with only the required permissions.

#### Configure Trust Relationships

1. Click on **Trust Relationships** tab
2. Click **Edit Trust Policy**
3. Copy and paste the following trust policy:

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": {
                "Service": "sagemaker.amazonaws.com"
            },
            "Action": "sts:AssumeRole"
        },
        {
            "Effect": "Allow",
            "Principal": {
                "Service": "cloudformation.amazonaws.com"
            },
            "Action": "sts:AssumeRole"
        }
    ]
}
```

4. Click **Update Policy**

### 3. Enable Docker on SageMaker Domain

1. Go to your **SageMaker Domain** and select **App Configuration**
2. Scroll down to the **Docker Configuration** section
3. Enable the option **Enable Docker on this domain**

### 4. Launch SageMaker Studio

1. In the SageMaker Domain console, click on **User Profiles**
2. Select your user profile
3. Click **Launch** → **Studio**
4. When SageMaker Studio opens, you can choose **Skip Tour** or explore the features

### 5. Set up JupyterLab Environment

1. Click on the **JupyterLab** icon in the left panel
2. Click **+ Create JupyterLab Space**
3. Name your space (e.g., "My-GenAI-Space")
4. Click **Run space** (keep default settings)
5. Wait for the space to show as **Running**
6. Click **Open JupyterLab now**

> **Important:** The ml.t3.medium instance is not free. You will be charged for every second it runs, so ensure you stop the space after completing the lab.

### 6. Clone the Repository and Set Up Environment

Open a terminal in JupyterLab and run the following commands:

```bash
# Clone the repository
git clone https://github.com/mehtasumti/Bedrcok-agentcore.git

# Navigate to the project directory
cd Bedrcok-agentcore

# Create and activate virtual environment using uv
uv python install 3.10
uv venv agentcore-samples --python 3.10
uv init

# Add required packages
uv add pip --active

# Install dependencies
pip install -r requirements.txt
```

## Labs

### Lab 1: Create Agent Prototype
Build a prototype of a customer support agent with three core tools:
- Return policy lookup
- Product information search  
- Web search for troubleshooting

**What you'll learn:** Basic agent creation with Strands Agents and tool integration

### Lab 2: Add Memory
Transform your "goldfish agent" into one that remembers customers across conversations.
- Persistent conversation history
- Customer preference extraction
- Cross-session context awareness

**What you'll learn:** AgentCore Memory for both short-term and long-term persistence

### Lab 3: Scale with Gateway & Identity
Move from local tools to shared, enterprise-ready services.
- Centralized tool management
- JWT-based authentication
- Integration with existing AWS Lambda functions

**What you'll learn:** AgentCore Gateway and AgentCore Identity for secure tool sharing

### Lab 4: Deploy to Production  
Deploy your agent to handle real traffic with full observability.
- Fully managed deployment
- Session Continuity and Session Isolation
- CloudWatch Observability integration

**What you'll learn:** AgentCore Runtime with production-grade observability

### Lab 5: Build Customer Interface
Create a web app customers can actually use.
- Streamlit-based chat interface
- Real-time response streaming
- Session management and authentication

**What you'll learn:** Frontend integration with secure agent endpoints

## Architecture Evolution

Watch your architecture grow from a simple local agent to a production system:

**Lab 1:** Local agent with embedded tools  
**Lab 2:** Agent + AgentCore Memory for persistence  
**Lab 3:** Agent + AgentCore Memory + AgentCore Gateway and AgentCore Identity for shared tools  
**Lab 4:** Deployment to AgentCore Runtime and observability with AgentCore Observability  
**Lab 5:** Customer-facing application with authentication

## Getting Started with Labs

1. Ensure you've completed all setup steps above
2. Configure AWS credentials (if not already configured)
3. Start with [Lab 1](lab-01-create-an-agent.ipynb)

Each lab builds on the previous one, but you can jump ahead if you understand the concepts.

## Important Notes

- **Cost Management:** Remember to stop your SageMaker Studio instances when not in use to avoid unnecessary charges
- **Security:** The Administrator Access policy is used for educational purposes. In production, use least-privilege IAM policies
- **Prerequisites:** Ensure Claude 3.7 Sonnet is enabled in your Bedrock account before starting

Ready to build? [Start with Lab 1 →](lab-01-create-an-agent.ipynb)
