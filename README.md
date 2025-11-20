# PostLo AI Financial Advisor

## Enterprise-Grade Multi-Agent Financial Planning Platform

![PostLo AI Financial Advisor](assets/alex.png)

PostLo AI Financial Advisor is a production-ready SaaS platform that leverages autonomous AI agents to provide comprehensive financial planning, portfolio analysis, and retirement projections. Built on AWS serverless architecture, the platform delivers enterprise-grade security, scalability, and performance.

### 🚀 Live Application

**Access the platform:** [https://d2hppyoilyf6w3.cloudfront.net](https://d2hppyoilyf6w3.cloudfront.net)

The application is deployed on AWS using CloudFront CDN, S3 static hosting, API Gateway, Lambda functions, and Aurora Serverless v2. Sign in with Clerk authentication to access AI-powered financial planning features.

### Key Features

- **Multi-Agent AI System**: Five specialized AI agents working in parallel to analyze portfolios, generate reports, create visualizations, and project retirement scenarios
- **Real-Time Portfolio Analysis**: Deep analysis of holdings, performance metrics, risk assessment, and allocation optimization
- **Interactive Visualizations**: Dynamic charts and graphs powered by Recharts
- **Retirement Projections**: Monte Carlo simulations for retirement readiness assessment
- **Enterprise Security**: Row-level data isolation, JWT authentication via Clerk, and AWS security best practices
- **Serverless Architecture**: Fully serverless infrastructure for cost optimization and automatic scaling

### Architecture Overview

The PostLo AI Financial Advisor platform uses a modern serverless architecture on AWS, combining AI services with cost-effective infrastructure. The system is built on a multi-agent architecture where specialized AI agents collaborate to provide comprehensive financial analysis.

#### System Components

1. **Frontend** (`frontend/`) - NextJS React application with Clerk authentication, deployed to S3 and served via CloudFront
2. **Backend API** (`backend/api/`) - FastAPI REST API running on Lambda, handling authentication and business logic
3. **AI Agents** (`backend/planner/`, `backend/tagger/`, `backend/reporter/`, `backend/charter/`, `backend/retirement/`) - Specialized Lambda functions using OpenAI Agents SDK with AWS Bedrock
4. **Research Agent** (`backend/researcher/`) - Autonomous research agent deployed on App Runner with web browsing capabilities
5. **Database** (`backend/database/`) - Aurora Serverless v2 PostgreSQL with Data API for serverless database access
6. **Infrastructure** (`terraform/`) - Infrastructure as Code organized by deployment phase
7. **Deployment Scripts** (`scripts/`) - Automated deployment and management tools

#### Key Infrastructure Components

- **S3 Vectors**: Native vector storage in S3 providing 90% cost reduction compared to traditional vector databases. Features sub-second similarity search, automatic optimization, and strongly consistent writes.

- **API Gateway**: REST API with API key authentication providing secure access to Lambda functions

- **Lambda Functions**: Serverless compute for document processing, agent orchestration, and API handling

- **App Runner**: Hosts the autonomous research agent with auto-scaling and HTTPS endpoint

- **SageMaker Serverless**: Generates 384-dimensional embeddings using sentence-transformers/all-MiniLM-L6-v2 model

- **AWS Bedrock**: Powers AI agents with Nova Pro model for research generation and analysis

- **EventBridge Scheduler**: Triggers automated research every 2 hours

- **Aurora Serverless v2**: PostgreSQL database with Data API for serverless database access

#### Agent Architecture

The platform employs a sophisticated multi-agent system where specialized AI agents collaborate to deliver comprehensive financial analysis:

**Financial Planner (Orchestrator)**
- Master coordinator managing the entire analysis workflow
- Receives user requests for portfolio analysis
- Identifies missing instrument data and delegates to specialized agents
- Retrieves relevant context from S3 Vectors knowledge base
- Compiles final analysis from all agent outputs

**InstrumentTagger**
- Automatically populates reference data for financial instruments
- Classifies instruments by asset class (equity, fixed income, etc.)
- Determines regional allocation and sector exposure
- Uses Structured Outputs for consistent data format

**Researcher (Independent Agent)**
- Autonomously gathers market intelligence and investment insights
- Runs independently on EventBridge schedule (every 2 hours)
- Browses financial websites for latest market trends
- Analyzes company news and earnings reports
- Continuously populates S3 Vectors knowledge base

**Report Writer**
- Generates comprehensive portfolio analysis narratives
- Analyzes portfolio composition and diversification
- Evaluates risk exposure and asset allocation
- Creates executive summaries and detailed analysis in markdown format

**Chart Maker**
- Transforms portfolio data into visual insights
- Calculates allocation percentages across dimensions
- Creates pie charts, bar charts, and sector visualizations
- Formats data for interactive Recharts components

**Retirement Specialist**
- Projects long-term financial outcomes
- Runs Monte Carlo simulations for probability analysis
- Factors in years until retirement and target income
- Creates projection charts and analyzes portfolio sustainability

#### Agent Collaboration Flow

1. **User Request** → Financial Planner receives portfolio analysis request
2. **Data Enrichment** → InstrumentTagger classifies any unknown instruments
3. **Knowledge Retrieval** → Financial Planner retrieves relevant context from S3 Vectors
4. **Parallel Processing** → Report Writer, Chart Maker, and Retirement Specialist execute simultaneously
5. **Result Compilation** → Financial Planner compiles all outputs into comprehensive analysis
6. **Independent Research** → Researcher agent continuously updates knowledge base on schedule

#### Data Flow

- **Portfolio Analysis Flow**: User → API Gateway → Lambda → Financial Planner → [Tagger, Reporter, Charter, Retirement] → Database
- **Research Flow**: EventBridge → Scheduler Lambda → Researcher Agent → Bedrock → API Gateway → S3 Vectors
- **Knowledge Integration**: Financial Planner → S3 Vectors (retrieve) → Contextual Analysis

### Technology Stack

- **Frontend**: Next.js 15, React 19, TypeScript, Tailwind CSS, Clerk Authentication
- **Backend**: FastAPI, Python 3.12, AWS Lambda, API Gateway
- **AI/ML**: OpenAI Agents SDK, AWS Bedrock (Nova Pro), LiteLLM, SageMaker Embeddings
- **Database**: Aurora Serverless v2 PostgreSQL, RDS Data API
- **Infrastructure**: Terraform, CloudFront, S3, Lambda, App Runner, SQS, Secrets Manager
- **Observability**: CloudWatch, LangFuse (optional)

### Project Structure

```
alex/
├── guides/              # Deployment guides and architecture documentation
├── backend/             # Agent code and Lambda functions
│   ├── planner/         # Orchestrator agent
│   ├── tagger/          # Instrument classification agent
│   ├── reporter/        # Portfolio analysis agent
│   ├── charter/         # Visualization agent
│   ├── retirement/      # Retirement projection agent
│   ├── researcher/      # Market research agent (App Runner)
│   ├── ingest/          # Document ingestion Lambda
│   ├── database/        # Shared database library
│   └── api/             # FastAPI backend for frontend
├── frontend/            # NextJS React application
├── terraform/           # Infrastructure as Code (independent directories)
└── scripts/             # Deployment and management scripts
```

### Security

- Row-level data isolation per user
- JWT authentication via Clerk
- Secrets stored in AWS Secrets Manager
- IAM roles with least-privilege access
- VPC endpoints for private AWS service access
- CloudWatch monitoring and alerting

### Contributing

This is a production enterprise system. For contributions, please follow the established patterns and ensure all tests pass before submitting changes.

### License

See LICENSE file for details.