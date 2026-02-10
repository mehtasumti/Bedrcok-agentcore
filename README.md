# 🤖 Production-Ready AI Agent with Amazon Bedrock AgentCore

[![AWS](https://img.shields.io/badge/AWS-Bedrock%20AgentCore-FF9900?style=flat&logo=amazon-aws)](https://aws.amazon.com/bedrock/)
[![Python](https://img.shields.io/badge/Python-3.10+-3776AB?style=flat&logo=python&logoColor=white)](https://www.python.org/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Tutorial](https://img.shields.io/badge/Tutorial-5%20Labs-blue.svg)](#-labs-overview)

> **A comprehensive hands-on tutorial demonstrating how to build enterprise-grade AI agents from prototype to production using Amazon Bedrock AgentCore**

Transform a basic chatbot into a production-ready customer support agent with persistent memory, secure tool integration, enterprise authentication, and full observability — all in 5 progressive labs.

---

## 📋 Table of Contents

- [Overview](#-overview)
- [What You'll Build](#-what-youll-build)
- [Key Features](#-key-features)
- [Architecture Evolution](#-architecture-evolution)
- [Prerequisites](#-prerequisites)
- [Quick Start](#-quick-start)
- [Labs Overview](#-labs-overview)
- [Tech Stack](#-tech-stack)
- [Project Structure](#-project-structure)
- [Cost Considerations](#-cost-considerations)
- [Troubleshooting](#-troubleshooting)
- [Cleanup](#-cleanup)
- [Contributing](#-contributing)
- [License](#-license)
- [Contact](#-contact)

---

## 🎯 Overview

Most AI agents today have a critical flaw: **no memory**. Every conversation starts from scratch, forcing users to repeat themselves and creating frustrating, impersonal experiences.

This tutorial solves that problem using **Amazon Bedrock AgentCore** — a comprehensive platform for building production-ready AI agents with:

- 🧠 **Persistent Memory** - Remember conversations across sessions (days, weeks, months)
- 🔧 **Enterprise Tools** - Secure integration with APIs, databases, and Lambda functions
- 🔐 **Identity Management** - Multi-tenant authentication and authorization
- ⚡ **Auto-Scaling** - Serverless production deployment handling 1 to 10,000+ users
- 📊 **Full Observability** - Comprehensive monitoring, tracing, and debugging

### Why This Tutorial Matters

**The Gap Between Prototype and Production:**

| Prototype | Production |
|-----------|------------|
| ❌ No memory | ✅ Persistent memory across months |
| ❌ Local tools only | ✅ Enterprise API integration |
| ❌ No authentication | ✅ JWT + OAuth2 security |
| ❌ Single user | ✅ Auto-scaling for thousands |
| ❌ No monitoring | ✅ Full observability |

**This Tutorial Bridges That Gap** with hands-on implementation of all five production requirements.

---

## 🏗️ What You'll Build

A **complete customer support agent** that evolves from a simple prototype to a production-ready system through 5 incremental labs.

### Final System Capabilities

| Capability | Description | Lab |
|------------|-------------|-----|
| 💬 **Conversational AI** | Natural language understanding via Claude 3.7 Sonnet | 1 |
| 🧠 **Dual Memory** | Short-term (session) + Long-term (persistent facts) | 2 |
| 🔧 **Custom Tools** | Product info, warranty checks, return policies, web search | 1-3 |
| 🔐 **JWT Authentication** | Secure access via Amazon Cognito | 3 |
| ⚡ **Auto-Scaling** | Handles 1 → 10,000+ concurrent users seamlessly | 4 |
| 📊 **Full Observability** | CloudWatch GenAI integration with distributed tracing | 4 |
| 💻 **Web Interface** | Customer-facing Streamlit application | 5 |

### Business Impact

- 📉 **Reduced Support Costs** - Automate repetitive inquiries (up to 70% of common questions)
- 📈 **Improved Satisfaction** - Personalized, context-aware responses
- ⚡ **Faster Resolution** - Instant access to customer history and preferences
- 🔒 **Compliance Ready** - Full audit trails and secure access controls

### Real-World Use Cases

This architecture is production-ready for:
- Customer support automation
- Technical troubleshooting assistants
- Sales enablement agents
- IT helpdesk automation
- HR policy assistants
- Insurance claims processing

---

## ✨ Key Features

### 1. 🧠 AgentCore Memory - The Brain That Never Forgets

**Problem:** Traditional AI agents are stateless. Every conversation = blank slate.

**Solution:** Dual-memory architecture
- **Short-term Memory:** Maintains context within current session
- **Long-term Memory:** Stores customer preferences across months

**Real Example:**
```
User Session 1 (January): "I prefer email updates"
[Agent stores preference in long-term memory]

User Session 2 (March): "What's the status of my order?"
Agent: "Welcome back! I'll send updates to your email as you prefer."
```

**Technical Implementation:**
- Automatic memory extraction from conversations
- Semantic storage with identity-based retrieval
- DynamoDB-backed persistence

---

### 2. 🔧 AgentCore Gateway - Universal Tool Connector

**Problem:** Agents need to access APIs, databases, CRMs—but building secure connections is complex.

**Solution:** Managed connectivity layer using **Model Context Protocol (MCP)**

Think of it as a **universal adapter** 🔌 for your AI agent:
- Connects to Lambda functions
- Integrates enterprise APIs
- Provides unified interface for hundreds of tools
- Handles authentication automatically

**What This Enables:**
- Share tools across multiple agents (no code duplication)
- Update tools once, deploy everywhere
- Semantic tool discovery and invocation
- Centralized security and access control

---

### 3. 🔐 AgentCore Identity - Enterprise Security Guardian

**Problem:** How do you ensure agents act on behalf of the right user? How do tools verify the caller?

**Solution:** Dual authentication system

**Authentication Flow:**
```
1. User logs in → Cognito issues JWT token
2. User sends request → Agent validates JWT
3. Agent needs tool → Gateway validates workload identity
4. Gateway calls API → Uses OAuth2 credentials
5. API returns data → Scoped to user's permissions
```

**Security Features:**
- Multi-tenant isolation
- Role-based access control (RBAC)
- Token caching for performance
- Audit trails for compliance

---

### 4. ⚡ AgentCore Runtime - Production Powerhouse

**Problem:** Your agent works on your laptop, but production is different:
- How to scale to 10,000 concurrent users?
- How to ensure 99.9% uptime?
- How to debug when things break?

**Solution:** Fully managed, serverless agent deployment

**What It Handles:**
- ☁️ **Auto-scaling:** Dynamically adjusts resources based on demand
- 🔄 **Session Management:** Isolates conversations per user
- 📊 **Load Balancing:** Distributes traffic intelligently
- 🛡️ **Error Recovery:** Automatic retries and fallbacks
- 🔒 **Security:** IAM-based access control

**Developer Experience:** Added **only 4 lines of code** to move from local prototype to production deployment.

---

### 5. 📊 AgentCore Observability - X-Ray Vision for AI

**Problem:** When an AI agent fails or behaves unexpectedly, debugging is nearly impossible.

**Solution:** Comprehensive telemetry using **OpenTelemetry + CloudWatch GenAI Observability**

**What You Can See:**
- 🔍 **Complete Request Traces:** User input → LLM reasoning → Tool calls → Response
- ⏱️ **Performance Metrics:** Response times, latency bottlenecks, success rates
- 🎯 **Error Patterns:** Where and why failures occur
- 💾 **Memory Access:** What's being stored and retrieved
- 🔧 **Tool Usage:** Which APIs are called, with what parameters

---

## 🔄 Architecture Evolution

Watch your architecture transform from a simple local agent to a production system:

### Lab 1: Basic Prototype
```
┌──────┐     ┌─────────────┐     ┌───────┐
│ User │────▶│ Local Agent │────▶│ Tools │
└──────┘     └─────────────┘     └───────┘
```
**Capabilities:** Basic conversation, local tools

---

### Lab 2: + Memory
```
┌──────┐     ┌───────┐     ┌────────────────┐
│ User │────▶│ Agent │────▶│ AgentCore      │
└──────┘     └───┬───┘     │ Memory         │
                 │          └────────────────┘
                 │          ┌───────┐
                 └─────────▶│ Tools │
                            └───────┘
```
**New Capabilities:** Conversation persistence, preference learning

---

### Lab 3: + Gateway & Identity
```
┌──────┐     ┌───────┐     ┌────────────────┐
│ User │────▶│ Agent │────▶│ AgentCore      │
└──────┘     └───┬───┘     │ Memory         │
                 │          └────────────────┘
                 │          ┌────────────────┐     ┌────────┐
                 ├─────────▶│ AgentCore      │────▶│ Lambda │
                 │          │ Gateway        │     │ Tools  │
                 │          └────────────────┘     └────────┘
                 │          ┌────────────────┐     ┌─────────┐
                 └─────────▶│ AgentCore      │────▶│ Cognito │
                            │ Identity       │     └─────────┘
                            └────────────────┘
```
**New Capabilities:** Secure tool sharing, JWT authentication, enterprise APIs

---

### Lab 4: + Production Runtime
```
┌──────┐     ┌────────────────────┐     ┌───────┐
│ User │────▶│ AgentCore Runtime  │────▶│ Agent │─┬─▶ Memory
└──────┘     │ (Auto-scaling)     │     └───────┘ ├─▶ Gateway
             └────────────────────┘               ├─▶ Identity
                        │                         └─▶ Tools
                        ▼
             ┌────────────────────┐
             │ AgentCore          │
             │ Observability      │
             └─────────┬──────────┘
                       ▼
             ┌────────────────────┐
             │ CloudWatch GenAI   │
             └────────────────────┘
```
**New Capabilities:** Serverless deployment, observability, auto-scaling

---

### Lab 5: + Customer Interface (Final)
```
┌──────┐     ┌─────────────┐     ┌────────────────────┐
│ User │────▶│ Streamlit   │────▶│ AgentCore Runtime  │
└──────┘     │ Web App     │     │ (Auto-scaling)     │
             └─────────────┘     └──────────┬─────────┘
                                            ▼
                                  ┌───────────────────┐
                                  │   Agent Stack     │
                                  │ ─────────────────│
                                  │ • Memory          │
                                  │ • Gateway         │
                                  │ • Identity        │
                                  │ • Tools           │
                                  │ • Observability   │
                                  └───────────────────┘
```
**Final Capabilities:** Complete customer-facing application with all production features

---

## 📋 Prerequisites

### Required

✅ **AWS Account** with Bedrock access  
✅ **Python 3.10+** installed locally  
✅ **AWS CLI** configured with appropriate credentials  
✅ **Claude 3.7 Sonnet** enabled in Amazon Bedrock  
✅ **SageMaker AI Domain** (for JupyterLab environment)  

### Recommended Knowledge

- Basic Python programming
- Familiarity with AWS services (Lambda, Cognito, CloudWatch)
- Understanding of REST APIs and authentication concepts
- Experience with Jupyter notebooks

### Skills You'll Develop

By completing this tutorial, you'll gain hands-on experience with:
- ✅ Agent orchestration frameworks (Strands Agents)
- ✅ LLM integration and prompt engineering
- ✅ Memory system architecture
- ✅ API gateway patterns (MCP)
- ✅ JWT and OAuth2 authentication
- ✅ Serverless deployment (containerization)
- ✅ Observability instrumentation (OpenTelemetry)
- ✅ Full-stack application development

---

## 🚀 Quick Start

### Option 1: SageMaker Studio (Recommended for Beginners)

#### Step 1: Set Up SageMaker Domain

1. **Navigate to Amazon SageMaker Console**
   - Go to AWS Console → SageMaker

2. **Create a New Domain**
   - Click "Create domain"
   - Choose **Quick setup** (recommended for this tutorial)
   - Follow the prompts to create your domain

3. **Configure IAM Role Permissions**
   - Go to **IAM Console** → **Roles**
   - Find the role attached to your SageMaker Domain
   - Click **Attach policies**
   - Search for and attach `AdministratorAccess` policy
   
   > ⚠️ **Security Note:** `AdministratorAccess` is used for educational purposes only. In production environments, always follow the principle of least privilege with custom IAM policies.

4. **Configure Trust Relationships**
   - In the IAM role, click **Trust relationships** tab
   - Click **Edit trust policy**
   - Replace with:

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": {
                "Service": [
                    "sagemaker.amazonaws.com",
                    "cloudformation.amazonaws.com"
                ]
            },
            "Action": "sts:AssumeRole"
        }
    ]
}
```

   - Click **Update policy**

5. **Enable Docker**
   - Go to your SageMaker Domain
   - Navigate to **App Configuration**
   - Scroll to **Docker Configuration**
   - Enable: **"Enable Docker on this domain"**

#### Step 2: Launch JupyterLab

1. In SageMaker Domain console, go to **User Profiles**
2. Select your user profile
3. Click **Launch** → **Studio**
4. In Studio, click the **JupyterLab** icon in left panel
5. Click **+ Create JupyterLab Space**
6. Name your space (e.g., "AgentCore-Workshop")
7. Click **Run space** (keep default settings)
8. Wait for status to show **Running**
9. Click **Open JupyterLab now**

> 💡 **Cost Note:** The ml.t3.medium instance costs ~$0.05/hour. Remember to stop your space after completing labs.

#### Step 3: Set Up Environment in JupyterLab

Open a terminal in JupyterLab and run:

```bash
# Clone the repository
git clone https://github.com/mehtasumti/Bedrcok-agentcore.git
cd Bedrcok-agentcore

# Create virtual environment using uv
uv python install 3.10
uv venv agentcore-samples --python 3.10
uv init

# Activate environment and install dependencies
uv add pip --active
pip install -r requirements.txt
```

#### Step 4: Verify Setup

```bash
# Test AWS credentials
aws sts get-caller-identity

# Verify Bedrock access and Claude 3.7 Sonnet
aws bedrock list-foundation-models --region us-east-1 | grep claude-3-7-sonnet

# Expected output should include: claude-3-7-sonnet-20250219
```

---

### Option 2: Local Development Setup

For experienced developers who prefer local development:

```bash
# Clone repository
git clone https://github.com/mehtasumti/Bedrcok-agentcore.git
cd Bedrcok-agentcore

# Create virtual environment
python3 -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Configure AWS credentials
aws configure
```

---

## 📖 Labs Overview

Complete these 5 progressive labs to build your production-ready agent. **Total time: ~2-3 hours**

---

### Lab 1: Create Agent Prototype

**⏱️ Time:** 20 minutes  
**📓 Notebook:** `lab-01-create-an-agent.ipynb`

#### What You'll Build
- Basic customer support agent using Strands Agents framework
- Three core tools:
  - `get_return_policy()` - Retrieve return policy information
  - `get_product_info()` - Look up product specifications
  - `get_technical_support()` - Access troubleshooting guides

#### What You'll Learn
- Agent initialization and configuration
- Tool creation using `@tool` decorator
- Local agent testing in Jupyter notebooks
- Conversation flow and orchestration

#### Key Concepts
- Agent orchestration patterns
- Tool calling mechanisms
- Prompt engineering for agents
- Function calling with LLMs

---

### Lab 2: Add Memory

**⏱️ Time:** 20 minutes  
**📓 Notebook:** `lab-02-agentcore-memory.ipynb`

#### What You'll Build
- Persistent conversation memory using AgentCore Memory
- Automatic customer preference extraction
- Short-term memory (session context)
- Long-term memory (persistent facts)

#### What You'll Learn
- AgentCore Memory service integration
- Memory hook configuration
- Session-based context retrieval
- Long-term fact storage patterns

#### Key Concepts
- Dual-memory architecture (short-term + long-term)
- Semantic storage and retrieval
- Identity-based memory scoping
- Memory extraction from conversations

#### Expected Output
```python
# Session 1
User: "I prefer email updates"
Agent: "Noted! I'll remember that you prefer email updates."

# Session 2 (3 weeks later)
User: "What's the status of my order?"
Agent: "Welcome back! I'll send updates via email as you prefer..."
```

---

### Lab 3: Scale with Gateway & Identity

**⏱️ Time:** 30 minutes  
**📓 Notebook:** `lab-03-agentcore-gateway.ipynb`

#### What You'll Build
- Centralized tool management via AgentCore Gateway
- JWT-based authentication with Amazon Cognito
- Lambda function integration for enterprise tools
- OAuth2 authentication flows

#### What You'll Learn
- Model Context Protocol (MCP) implementation
- Inbound authentication (user → agent)
- Outbound authentication (agent → APIs)
- Tool sharing across multiple agents

#### Key Concepts
- API gateway patterns
- Workload identity management
- Token exchange and caching
- Secure tool invocation

---

### Lab 4: Deploy to Production

**⏱️ Time:** 30 minutes  
**📓 Notebook:** `lab-04-agentcore-runtime.ipynb`

#### What You'll Build
- Production deployment to AgentCore Runtime
- Comprehensive observability with CloudWatch GenAI
- Auto-scaling serverless infrastructure
- Session isolation and continuity

#### What You'll Learn
- Container-based agent deployment (Docker)
- OpenTelemetry instrumentation
- Distributed tracing patterns
- Production session management

#### Key Concepts
- Serverless architecture
- Horizontal auto-scaling
- Request tracing and monitoring
- Performance optimization

---

### Lab 5: Build Customer Interface

**⏱️ Time:** 20 minutes  
**📓 Notebook:** `lab-05-frontend.ipynb`

#### What You'll Build
- Streamlit-based web application
- Real-time response streaming
- User authentication UI
- Session management interface

#### What You'll Learn
- Frontend integration with AgentCore Runtime
- Streaming response handling
- WebSocket connections
- User experience design for AI agents

#### Expected Output
- Live web application at `http://localhost:8501`
- Real-time streaming responses
- User login/logout functionality
- Conversation history display

---

### 🎓 Bonus Lab: Deep Dive into Observability (Optional)

**⏱️ Time:** 30 minutes  
**📓 Notebook:** `Optional-lab-agentcore-observability.ipynb`

Manual OpenTelemetry instrumentation without AgentCore Runtime.

---

## 🛠️ Tech Stack

### AWS Services

| Service | Purpose | Used In Labs |
|---------|---------|--------------|
| **Amazon Bedrock** | LLM orchestration (Claude 3.7 Sonnet) | All Labs |
| **AgentCore Memory** | Persistent conversation storage | Lab 2+ |
| **AgentCore Gateway** | MCP-based tool connectivity | Lab 3+ |
| **AgentCore Identity** | JWT authentication & authorization | Lab 3+ |
| **AgentCore Runtime** | Serverless agent deployment | Lab 4+ |
| **AgentCore Observability** | Monitoring & distributed tracing | Lab 4+ |
| **AWS Lambda** | Backend tool execution | Lab 3+ |
| **Amazon Cognito** | User identity management | Lab 3+ |
| **Amazon CloudWatch** | Logging, metrics, and dashboards | Lab 4+ |
| **Amazon DynamoDB** | Memory persistence layer | Lab 2+ |
| **SageMaker Studio** | Development environment | All Labs |

### Frameworks & Libraries

```python
# Core Agent Framework
strands-agents          # Agent orchestration

# AWS SDKs
boto3                   # AWS SDK for Python
botocore                # Low-level AWS SDK

# Observability
opentelemetry-sdk       # OpenTelemetry instrumentation
opentelemetry-api       # OpenTelemetry API

# Authentication
python-jose[cryptography]  # JWT token handling

# Web Framework
streamlit               # Web UI framework

# Utilities
requests                # HTTP client
python-dotenv           # Environment variable management
pydantic                # Data validation
```

### Model Information

**Primary Model:** Claude 3.7 Sonnet (`claude-3-7-sonnet-20250219`)
- Context window: 200K tokens
- Max output: 8K tokens
- Strengths: Advanced reasoning, tool use, long context

---

## 📁 Project Structure

```
Bedrcok-agentcore/
│
├── README.md                                     # This file
├── LICENSE                                       # MIT License
├── requirements.txt                              # Python dependencies
├── .gitignore                                    # Git ignore rules
│
├── lab-01-create-an-agent.ipynb                 # Lab 1: Agent prototype
├── lab-02-agentcore-memory.ipynb                # Lab 2: Add memory
├── lab-03-agentcore-gateway.ipynb               # Lab 3: Gateway & identity
├── lab-04-agentcore-runtime.ipynb               # Lab 4: Production deployment
├── lab-05-frontend.ipynb                        # Lab 5: Customer interface
├── Optional-lab-agentcore-observability.ipynb   # Bonus: Deep observability
├── lab-06-cleanup-COMPLETE.ipynb                # Cleanup instructions
│
├── docs/                                         # Documentation
│   ├── images/                                   # Architecture diagrams
│   └── guides/                                   # Additional guides
│
├── src/                                          # Source code
│   ├── agents/                                   # Agent implementations
│   ├── tools/                                    # Tool definitions
│   ├── memory/                                   # Memory utilities
│   ├── gateway/                                  # Gateway configuration
│   ├── auth/                                     # Authentication utilities
│   ├── observability/                            # Observability setup
│   ├── frontend/                                 # Streamlit app
│   └── utils/                                    # Shared utilities
│
├── tests/                                        # Unit tests
│   ├── test_agent.py
│   ├── test_tools.py
│   ├── test_memory.py
│   └── test_auth.py
│
├── lambda/                                       # Lambda functions
│   ├── web_search/
│   └── check_warranty/
│
└── cloudformation/                               # IaC templates
    ├── gateway-stack.yaml
    ├── runtime-stack.yaml
    └── observability-stack.yaml
```

---

## 💰 Cost Considerations

### Workshop Cost Breakdown

**Total Estimated Cost: $5-10** (for completing all 5 labs in 2-3 hours)

| Service | Cost | Notes |
|---------|------|-------|
| **SageMaker Studio** | ~$0.10-0.15 | ml.t3.medium @ $0.05/hour for 2-3 hours |
| **Amazon Bedrock** | ~$3-5 | Claude 3.7 Sonnet API calls (~100-200 requests) |
| **Lambda** | <$0.01 | Within free tier (1M requests/month free) |
| **Cognito** | $0 | Free tier (50,000 MAU free) |
| **CloudWatch** | <$0.50 | Basic logs and metrics (5GB free) |
| **DynamoDB** | <$0.50 | On-demand pricing for memory storage |

### Cost Optimization Tips

1. **Stop SageMaker Instances Immediately After Labs**
2. **Use Free Tier Limits** where available
3. **Clean Up Resources After Completion** (Lab 6)
4. **Set Up Billing Alerts** in AWS Console
5. **Monitor Costs in Real-Time** via AWS Cost Explorer

---

## 🐛 Troubleshooting

### Common Issues and Solutions

#### 1. Bedrock Access Denied

**Solution:**
```bash
# Verify Claude 3.7 Sonnet is enabled
aws bedrock list-foundation-models --region us-east-1 | grep claude-3-7-sonnet

# Enable model access in Bedrock console
# Go to: AWS Console → Bedrock → Model access → Request model access
```

#### 2. SageMaker Permission Errors

**Solution:**
- Verify IAM role has `AdministratorAccess` or required permissions
- Check trust relationships are correctly configured
- Ensure you're using the correct AWS account/region

#### 3. Memory Not Persisting

**Solution:**
```python
# Verify AgentCore Memory is configured
import boto3
client = boto3.client('bedrock-agent')
response = client.list_agent_memories()
print(response)
```

#### 4. Gateway Authentication Failures

**Solution:**
- Verify Cognito user pool configuration
- Check JWT token is valid and not expired
- Ensure token hasn't expired (typically 1 hour)

#### 5. Docker Build Failures

**Solution:**
- Verify Docker is enabled in SageMaker Domain settings
- Restart JupyterLab space
- Check Docker is running: `docker --version`

### Getting Help

- 📖 [AWS Documentation](https://docs.aws.amazon.com/bedrock/)
- 💬 [GitHub Issues](https://github.com/mehtasumti/Bedrcok-agentcore/issues)
- 🎓 [Community Forum](https://www.skool.com/k21academy/issue-qa-lab-build-prod-ready-ai-agents-with-bedrock-agentcore-post-here)

---

## 🧹 Cleanup

**Important:** Clean up resources after completing the tutorial to avoid ongoing charges.

### Automated Cleanup

```bash
# Run the cleanup notebook
jupyter notebook lab-06-cleanup-COMPLETE.ipynb
```

### Manual Cleanup Checklist

- [ ] Stop SageMaker Studio instances
- [ ] Delete AgentCore Runtime deployments
- [ ] Remove Lambda functions
- [ ] Delete Cognito user pools
- [ ] Clear CloudWatch log groups
- [ ] Remove test IAM roles

---

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create feature branch (`git checkout -b feature/amazing-feature`)
3. Commit changes (`git commit -m 'Add amazing feature'`)
4. Push to branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Areas for Contribution

- 🐛 Bug fixes
- 📖 Documentation improvements
- ✨ New features or tools
- 🧪 Test coverage
- 🎨 UI/UX enhancements

---

## 📄 License

This project is licensed under the MIT License - see [LICENSE](LICENSE) file for details.

---

## ⚠️ Important Disclaimers

### Educational Purpose

> **This tutorial is designed for educational purposes** to demonstrate Amazon Bedrock AgentCore capabilities. It is **NOT intended for direct use in production environments** without proper security hardening and architectural review.

### Security Notice

> **IAM Policies:** The `AdministratorAccess` policy used in this tutorial is **overly permissive** and provided for educational simplicity only. In production, always follow the principle of least privilege.

### Cost Warning

> **AWS Charges:** This workshop uses paid AWS services. While designed to minimize costs (~$5-10), you are responsible for monitoring your AWS billing dashboard and cleaning up resources.

---

## 🌟 Acknowledgments

- **AWS Team** - For Amazon Bedrock AgentCore services
- **Anthropic** - For Claude 3.7 Sonnet LLM
- **Strands Agents** - For agent orchestration framework
- **OpenTelemetry** - For observability instrumentation
- **Streamlit** - For web application framework

---

## 📞 Contact

**Author:** Mehta Sumti
- GitHub: [@mehtasumti](https://github.com/mehtasumti)
- Repository: [Bedrcok-agentcore](https://github.com/mehtasumti/Bedrcok-agentcore)

### Support Channels

- **GitHub Issues:** [Report bugs or request features](https://github.com/mehtasumti/Bedrcok-agentcore/issues)
- **Community Forum:** [Skool K21 Academy](https://www.skool.com/k21academy)
- **Discussions:** [GitHub Discussions](https://github.com/mehtasumti/Bedrcok-agentcore/discussions)

---

## 🎓 What's Next?

After completing this tutorial:

1. **Extend Functionality** - Add more tools (CRM, ticketing)
2. **Production Readiness** - Security hardening, performance optimization
3. **Advanced Features** - Multi-agent systems, advanced observability
4. **Share Your Experience** - Write blog posts, create tutorials

---

## 🚀 Ready to Begin?

### Start Your Journey

**[→ Start Lab 1: Create Agent Prototype](lab-01-create-an-agent.ipynb)**

---

<div align="center">

**Made with ❤️ for the AI Engineering Community**

⭐ Star this repository if you find it helpful!

🔗 Share with fellow AI engineers

💬 Join the discussion

</div>

---

**Last Updated:** February 2025  
**Version:** 1.0.0  
**Status:** ✅ Production Ready (for educational purposes)
