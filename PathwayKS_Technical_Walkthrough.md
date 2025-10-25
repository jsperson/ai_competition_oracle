# PathwayKS Technical Walkthrough
## Architecture, Tech Stack, and Implementation Guide

**Document Version:** 1.0
**Date:** October 2025
**Prepared for:** Kansas Department of Labor - Oracle Challenge

---

## Table of Contents

1. [System Overview](#1-system-overview)
2. [Technology Stack](#2-technology-stack)
3. [Architecture Design](#3-architecture-design)
4. [Core Components](#4-core-components)
5. [AI/ML Pipeline](#5-aiml-pipeline)
6. [Integration Architecture](#6-integration-architecture)
7. [Data Models](#7-data-models)
8. [Security & Compliance](#8-security--compliance)
9. [Deployment & Infrastructure](#9-deployment--infrastructure)
10. [Development Workflow](#10-development-workflow)
11. [Scalability & Performance](#11-scalability--performance)
12. [Implementation Roadmap](#12-implementation-roadmap)

---

## 1. System Overview

### 1.1 High-Level Architecture

PathwayKS is built as a modern, cloud-native application using a microservices architecture. The system consists of:

- **Frontend Layer:** Progressive Web App (PWA) and future mobile apps
- **API Gateway:** Central entry point for all client requests
- **Microservices Layer:** Independent services for user management, pathway matching, program catalog, job matching, and integrations
- **Data Layer:** Polyglot persistence with PostgreSQL, MongoDB, Redis, and Elasticsearch
- **Integration Layer:** Connections to partner systems (KansasWorks, training providers, employers)
- **AI/ML Pipeline:** Machine learning models for pathway matching and recommendations

### 1.2 Design Principles

1. **API-First:** All services expose RESTful APIs; frontend is a consumer
2. **Microservices:** Loosely coupled services that can scale independently
3. **Cloud-Native:** Designed for cloud deployment with auto-scaling and high availability
4. **Security-First:** Authentication, authorization, encryption at every layer
5. **Data-Driven:** Comprehensive analytics and logging for continuous improvement
6. **Mobile-First:** Responsive design prioritizing mobile experience
7. **Accessibility:** WCAG 2.1 Level AA compliance for inclusive access

### 1.3 Technology Decision Rationale

**Why Node.js for Backend?**
- Fast, event-driven architecture suitable for I/O-heavy operations
- Large ecosystem of libraries for integrations
- Same language (JavaScript/TypeScript) as frontend reduces context switching
- Excellent for API gateway and real-time features

**Why Python for AI/ML?**
- Industry standard for machine learning and data science
- Rich ecosystem (TensorFlow, scikit-learn, pandas, NumPy)
- Fast development cycle for model experimentation
- Strong community support

**Why PostgreSQL + MongoDB?**
- PostgreSQL for structured, relational data (users, transactions)
- MongoDB for flexible, document-based data (program catalog with varying schemas)
- Right tool for the right data model

**Why React.js?**
- Component-based architecture promotes reusability
- Large talent pool and community support
- Next.js framework adds SSR, routing, and optimization
- Excellent performance and SEO

**Why AWS GovCloud?**
- Compliance requirements for government data
- Proven reliability and security
- Comprehensive service offerings
- Government-specific support and certifications

---

## 2. Technology Stack

### 2.1 Frontend Stack

**Core Framework:**
- **React 18.x:** UI library for component-based development
- **Next.js 14.x:** React framework with SSR, SSG, and API routes
- **TypeScript 5.x:** Type safety and developer productivity

**State Management:**
- **Redux Toolkit:** Global state management
- **React Query:** Server state management and caching
- **Context API:** Local state for themes, auth, etc.

**UI Components:**
- **Tailwind CSS:** Utility-first CSS framework
- **Headless UI:** Accessible component primitives
- **Radix UI:** Low-level UI component library
- **Framer Motion:** Animation library

**Forms & Validation:**
- **React Hook Form:** Performant form management
- **Zod:** TypeScript-first schema validation
- **yup:** Alternative schema validation

**Data Visualization:**
- **Recharts:** Charting library for analytics dashboards
- **D3.js:** Custom visualizations (pathway diagrams)

**Build & Development Tools:**
- **Vite:** Fast build tool and dev server
- **ESLint + Prettier:** Code quality and formatting
- **Husky:** Git hooks for pre-commit checks
- **Jest + React Testing Library:** Unit and integration testing
- **Cypress:** End-to-end testing

### 2.2 Backend Stack

**Core Framework (Node.js Services):**
- **Node.js 20.x LTS:** Runtime environment
- **Express.js 4.x:** Web framework for API development
- **TypeScript 5.x:** Type safety across backend

**Core Framework (Python Services):**
- **Python 3.11+:** Runtime environment
- **FastAPI:** Modern, fast web framework for APIs
- **Pydantic:** Data validation using Python type annotations

**API & Communication:**
- **GraphQL (Apollo Server):** Flexible data querying
- **REST:** Traditional RESTful endpoints where appropriate
- **WebSockets (Socket.io):** Real-time communication
- **gRPC:** Inter-service communication

**Authentication & Authorization:**
- **Auth0:** Identity management platform
- **JWT:** Token-based authentication
- **OAuth 2.0:** Third-party integrations
- **Passport.js:** Authentication middleware

**Data Access:**
- **Prisma:** TypeScript ORM for PostgreSQL
- **Mongoose:** MongoDB ODM
- **ioredis:** Redis client for caching
- **Elasticsearch client:** Full-text search

**Background Jobs:**
- **Bull:** Redis-based queue for Node.js
- **Celery:** Distributed task queue for Python
- **Cron jobs:** Scheduled tasks (AWS EventBridge)

**API Documentation:**
- **OpenAPI 3.0 (Swagger):** API specification
- **Redoc:** API documentation UI
- **Postman:** API testing and collaboration

### 2.3 Data Layer

**Primary Database (Relational):**
- **PostgreSQL 15.x:** User data, transactions, audit logs
  - Extensions: PostGIS (location data), pg_trgm (fuzzy search)
  - Connection pooling: PgBouncer
  - Replication: Streaming replication for read replicas

**Secondary Database (Document):**
- **MongoDB 7.x:** Program catalog, flexible schemas
  - Replica sets for high availability
  - Sharding for horizontal scalability
  - Atlas managed service option

**Caching Layer:**
- **Redis 7.x:** Session storage, caching, pub/sub
  - Redis Cluster for scalability
  - Redis Sentinel for high availability
  - Use cases: user sessions, API response caching, rate limiting

**Search Engine:**
- **Elasticsearch 8.x:** Full-text search across programs and jobs
  - Kibana for log visualization
  - Logstash for log ingestion (ELK stack)

### 2.4 AI/ML Stack

**Machine Learning Frameworks:**
- **TensorFlow 2.x:** Deep learning models
- **scikit-learn:** Classical ML algorithms (random forests, SVM, etc.)
- **XGBoost:** Gradient boosting for tabular data
- **Pandas + NumPy:** Data manipulation and numerical computing

**Natural Language Processing:**
- **spaCy:** NLP for skills extraction from resumes/job descriptions
- **Hugging Face Transformers:** Pre-trained language models
- **NLTK:** Text processing utilities

**Feature Engineering:**
- **Feature-engine:** Feature engineering library
- **Category Encoders:** Categorical variable encoding

**Model Training & Experimentation:**
- **MLflow:** Model tracking and registry
- **Weights & Biases:** Experiment tracking
- **Jupyter Notebooks:** Interactive development

**Model Serving:**
- **TensorFlow Serving:** Production ML serving
- **TorchServe:** Alternative model serving
- **FastAPI:** Custom model endpoints

**Data Processing:**
- **Apache Spark (optional for large-scale):** Distributed data processing
- **Dask:** Parallel computing library for Python
- **Airflow:** Workflow orchestration for data pipelines

### 2.5 DevOps & Infrastructure

**Cloud Platform:**
- **AWS GovCloud:** Government-compliant cloud environment
  - EC2: Compute instances
  - ECS/Fargate: Container orchestration
  - Lambda: Serverless functions
  - RDS: Managed PostgreSQL
  - DocumentDB: MongoDB-compatible service
  - ElastiCache: Managed Redis
  - S3: Object storage
  - CloudFront: CDN
  - Route 53: DNS
  - Cognito: User authentication (alternative to Auth0)
  - SES: Email service
  - SNS/SQS: Messaging and queuing
  - CloudWatch: Monitoring and logging
  - EventBridge: Event-driven automation

**Containerization:**
- **Docker:** Application containerization
- **Docker Compose:** Local development orchestration

**Container Orchestration:**
- **AWS ECS/Fargate:** Managed container service
- **Kubernetes (future):** If multi-cloud or advanced orchestration needed

**CI/CD:**
- **GitHub Actions:** CI/CD workflows
- **AWS CodePipeline:** Alternative CI/CD
- **AWS CodeBuild:** Build service
- **AWS CodeDeploy:** Deployment service

**Infrastructure as Code:**
- **Terraform:** Cloud infrastructure provisioning
- **AWS CloudFormation:** Alternative IaC for AWS
- **Ansible:** Configuration management

**Monitoring & Observability:**
- **Datadog:** Application performance monitoring
- **Sentry:** Error tracking and monitoring
- **CloudWatch:** AWS-native monitoring
- **ELK Stack:** Log aggregation and analysis
- **Prometheus + Grafana (optional):** Metrics and dashboards

**Security:**
- **AWS WAF:** Web application firewall
- **AWS Shield:** DDoS protection
- **AWS Secrets Manager:** Secret storage
- **AWS KMS:** Key management
- **Snyk:** Vulnerability scanning
- **OWASP ZAP:** Security testing

### 2.6 Development Tools

**Version Control:**
- **Git:** Source control
- **GitHub:** Code hosting and collaboration
- **GitHub Projects:** Issue tracking and project management

**Code Quality:**
- **SonarQube:** Code quality and security analysis
- **ESLint:** JavaScript/TypeScript linting
- **Pylint/Flake8:** Python linting
- **Black:** Python code formatting
- **Prettier:** JavaScript/TypeScript formatting

**Testing:**
- **Jest:** JavaScript unit testing
- **Pytest:** Python unit testing
- **Cypress:** E2E testing
- **Postman/Newman:** API testing
- **k6:** Load testing

**Documentation:**
- **Storybook:** Component documentation
- **Docusaurus:** Technical documentation site
- **Markdown:** Developer documentation

**Communication:**
- **Slack:** Team communication
- **Zoom:** Video conferencing
- **Miro:** Collaborative whiteboarding
- **Notion:** Knowledge base

---

## 3. Architecture Design

### 3.1 System Architecture Diagram

```
┌─────────────────────────────────────────────────────────────────────┐
│                          CLIENT LAYER                               │
│                                                                     │
│  ┌──────────────────┐         ┌──────────────────┐                 │
│  │   Web Browser    │         │   Mobile App     │                 │
│  │  (React/Next.js) │         │ (React Native)   │                 │
│  └────────┬─────────┘         └────────┬─────────┘                 │
│           │                             │                           │
└───────────┼─────────────────────────────┼───────────────────────────┘
            │                             │
            └──────────────┬──────────────┘
                           │
┌──────────────────────────▼────────────────────────────────────────┐
│                     CDN (CloudFront)                               │
└──────────────────────────┬────────────────────────────────────────┘
                           │
┌──────────────────────────▼────────────────────────────────────────┐
│                   API GATEWAY (Node.js/Express)                    │
│                                                                    │
│  ┌────────────────┐  ┌────────────────┐  ┌────────────────┐      │
│  │Authentication  │  │Rate Limiting   │  │  Request       │      │
│  │   (Auth0/JWT)  │  │                │  │  Routing       │      │
│  └────────────────┘  └────────────────┘  └────────────────┘      │
└────────┬────────┬────────┬────────┬────────┬────────┬────────────┘
         │        │        │        │        │        │
    ┌────▼───┐┌──▼───┐┌───▼───┐┌───▼───┐┌──▼────┐┌──▼────────┐
    │ User   ││Match-││Program││  Job  ││Barrier││Integration│
    │Service ││ing   ││Service││Service││Service││  Service  │
    │(Node)  ││Svc   ││(Node) ││(Node) ││(Node) ││  (Node)   │
    │        ││(Py)  ││       ││       ││       ││           │
    └────┬───┘└──┬───┘└───┬───┘└───┬───┘└──┬────┘└──┬────────┘
         │       │        │        │       │        │
         │       │        │        │       │        │
┌────────▼───────▼────────▼────────▼───────▼────────▼──────────────┐
│                      DATA LAYER                                    │
│                                                                    │
│  ┌──────────┐  ┌──────────┐  ┌─────────┐  ┌──────────────────┐  │
│  │PostgreSQL│  │ MongoDB  │  │  Redis  │  │  Elasticsearch   │  │
│  │  (RDS)   │  │(DocDB)   │  │(ElastiC)│  │   (Managed)      │  │
│  │          │  │          │  │         │  │                  │  │
│  │ Users    │  │ Programs │  │Sessions │  │ Search Index     │  │
│  │ Tracking │  │ Jobs     │  │Cache    │  │ Programs & Jobs  │  │
│  │ Audit    │  │ Partners │  │Pub/Sub  │  │                  │  │
│  └──────────┘  └──────────┘  └─────────┘  └──────────────────┘  │
└────────────────────────────────────────────────────────────────────┘
         │                              │
┌────────▼──────────────────────────────▼──────────────────────────┐
│                   AI/ML PIPELINE                                  │
│                                                                   │
│  ┌─────────────┐  ┌─────────────┐  ┌──────────────────────┐     │
│  │ Data Prep   │  │   Model     │  │   Model Serving      │     │
│  │ (Airflow)   │→ │  Training   │→ │  (TF Serving/FastAPI)│     │
│  │             │  │(TensorFlow) │  │                      │     │
│  └─────────────┘  └─────────────┘  └──────────────────────┘     │
└───────────────────────────────────────────────────────────────────┘
         │
┌────────▼──────────────────────────────────────────────────────────┐
│                   INTEGRATION LAYER                                │
│                                                                    │
│  ┌────────────┐  ┌────────────┐  ┌────────────┐  ┌────────────┐ │
│  │KansasWorks │  │  WSU Tech  │  │ Butler CC  │  │  Employer  │ │
│  │    API     │  │    API     │  │    API     │  │  ATS APIs  │ │
│  └────────────┘  └────────────┘  └────────────┘  └────────────┘ │
│                                                                    │
│  ┌────────────┐  ┌────────────┐  ┌────────────┐  ┌────────────┐ │
│  │  Payment   │  │ Childcare  │  │  Transport │  │   Email    │ │
│  │   APIs     │  │    APIs    │  │    APIs    │  │ (SES/SMTP) │ │
│  └────────────┘  └────────────┘  └────────────┘  └────────────┘ │
└───────────────────────────────────────────────────────────────────┘
```

### 3.2 Microservices Architecture

**Service: User Service**
- Responsibilities:
  - User registration and authentication
  - Profile management
  - Skills inventory
  - Preferences and settings
- Technology: Node.js + Express + PostgreSQL
- APIs:
  - POST /api/users/register
  - POST /api/users/login
  - GET /api/users/profile
  - PUT /api/users/profile
  - POST /api/users/skills

**Service: Matching Service**
- Responsibilities:
  - Pathway recommendation engine
  - Skills-to-program matching
  - AI/ML model inference
  - Recommendation ranking
- Technology: Python + FastAPI + TensorFlow
- APIs:
  - POST /api/matching/recommendations
  - GET /api/matching/pathway/{id}
  - POST /api/matching/feedback
- ML Models:
  - Collaborative filtering model
  - Content-based filtering model
  - Hybrid recommendation model

**Service: Program Catalog Service**
- Responsibilities:
  - Program data management
  - Search and filtering
  - Program details and metadata
  - Training provider information
- Technology: Node.js + Express + MongoDB + Elasticsearch
- APIs:
  - GET /api/programs/search
  - GET /api/programs/{id}
  - POST /api/programs (admin)
  - PUT /api/programs/{id} (admin)

**Service: Job Service**
- Responsibilities:
  - Job listing aggregation
  - Job search and matching
  - Application tracking
  - Employer connections
- Technology: Node.js + Express + MongoDB
- APIs:
  - GET /api/jobs/search
  - GET /api/jobs/{id}
  - POST /api/jobs/apply
  - GET /api/jobs/applications

**Service: Barrier Navigation Service**
- Responsibilities:
  - Eligibility checking
  - Assistance program matching
  - Application guidance
  - Support service connections
- Technology: Node.js + Express + PostgreSQL
- APIs:
  - POST /api/barriers/assess
  - GET /api/barriers/programs
  - POST /api/barriers/apply
  - GET /api/barriers/status

**Service: Integration Service**
- Responsibilities:
  - External API connections
  - Data synchronization
  - Webhook handling
  - Legacy system integration
- Technology: Node.js + Express
- Integration Patterns:
  - REST API clients
  - SFTP/batch file processing
  - Web scraping (when APIs unavailable)
  - Event-driven webhooks

**Service: Notification Service**
- Responsibilities:
  - Email notifications
  - SMS alerts
  - Push notifications (mobile)
  - In-app notifications
- Technology: Node.js + Express + SES/SNS
- APIs:
  - POST /api/notifications/send
  - GET /api/notifications/user/{id}
  - PUT /api/notifications/{id}/read

**Service: Analytics Service**
- Responsibilities:
  - User behavior tracking
  - Conversion funnel analysis
  - Partner performance metrics
  - Impact measurement
- Technology: Python + FastAPI + PostgreSQL
- Tools: Amplitude, Mixpanel, or custom

### 3.3 Data Flow

**User Registration & Assessment Flow:**
```
1. User submits registration form (email, password, basic info)
2. Frontend → API Gateway → User Service
3. User Service validates data and creates account in PostgreSQL
4. User Service returns JWT token
5. User redirected to skills assessment
6. User completes assessment (15-20 questions)
7. Frontend → API Gateway → User Service (save skills)
8. User Service stores skills in PostgreSQL
9. Frontend → API Gateway → Matching Service
10. Matching Service:
    - Fetches user profile and skills
    - Runs ML model inference
    - Queries Program Catalog Service for matching programs
    - Ranks recommendations
    - Returns top 3-5 pathways
11. Frontend displays pathway recommendations
```

**Pathway Selection & Enrollment Flow:**
```
1. User selects a pathway
2. Frontend → API Gateway → Barrier Navigation Service
3. Barrier Service:
    - Checks eligibility for financial assistance
    - Identifies transportation options
    - Identifies childcare assistance
    - Returns assistance programs
4. Frontend displays barrier navigator
5. User confirms selections
6. Frontend → API Gateway → Integration Service
7. Integration Service:
    - Calls training provider API to submit application
    - Calls assistance program APIs to submit applications
    - Schedules workforce center appointment
8. Integration Service returns confirmation
9. Notification Service sends confirmation emails
10. User Service updates user status to "enrolled"
```

**Job Matching & Placement Flow:**
```
1. User completes training program
2. Training provider API webhook → Integration Service
3. Integration Service updates user record (credential earned)
4. Job Service triggered to find matching jobs:
    - Queries MongoDB for jobs matching credential
    - Filters by location preference
    - Ranks by salary and match score
5. Notification Service alerts user of job matches
6. User browses jobs and applies
7. Frontend → API Gateway → Job Service (track application)
8. Integration Service forwards application to employer ATS
9. Job Service tracks application status
10. Notification Service sends updates (interview scheduled, offer, etc.)
```

---

## 4. Core Components

### 4.1 Frontend Components

**Component Hierarchy:**
```
App
├── Layout
│   ├── Header
│   │   ├── Logo
│   │   ├── Navigation
│   │   └── UserMenu
│   ├── Sidebar (conditional)
│   ├── Main Content
│   └── Footer
├── Pages
│   ├── Home
│   ├── Assessment
│   │   ├── SkillsInventory
│   │   ├── InterestsSelector
│   │   ├── ConstraintsForm
│   │   └── BarrierAssessment
│   ├── Recommendations
│   │   ├── PathwayCard (x3-5)
│   │   ├── ComparisonTable
│   │   └── PathwayDetails
│   ├── ProgramCatalog
│   │   ├── SearchBar
│   │   ├── FilterPanel
│   │   ├── ProgramGrid
│   │   └── ProgramDetail
│   ├── BarrierNavigator
│   │   ├── EligibilityChecker
│   │   ├── AssistancePrograms
│   │   └── ApplicationTracker
│   ├── Dashboard
│   │   ├── ProgressTimeline
│   │   ├── NextSteps
│   │   ├── Messages
│   │   └── RecommendedJobs
│   ├── Jobs
│   │   ├── JobSearch
│   │   ├── JobGrid
│   │   ├── JobDetail
│   │   └── ApplicationTracker
│   └── Profile
│       ├── PersonalInfo
│       ├── SkillsView
│       ├── Credentials
│       └── Settings
└── Shared Components
    ├── Button
    ├── Input
    ├── Card
    ├── Modal
    ├── Toast
    ├── Loading
    └── Error
```

**Key Features:**
- Responsive design (mobile-first)
- Progressive Web App (PWA) with offline support
- Lazy loading for optimal performance
- Server-side rendering (SSR) for SEO
- Accessibility (WCAG 2.1 AA)
- Multi-language support (i18n)

### 4.2 Backend API Endpoints

**User Service Endpoints:**
```
POST   /api/v1/users/register
POST   /api/v1/users/login
POST   /api/v1/users/logout
GET    /api/v1/users/me
PUT    /api/v1/users/me
GET    /api/v1/users/{id}
PUT    /api/v1/users/{id}
DELETE /api/v1/users/{id}

POST   /api/v1/users/skills
GET    /api/v1/users/skills
PUT    /api/v1/users/skills
POST   /api/v1/users/interests
GET    /api/v1/users/interests
POST   /api/v1/users/constraints
GET    /api/v1/users/constraints
```

**Matching Service Endpoints:**
```
POST   /api/v1/matching/recommendations
GET    /api/v1/matching/recommendations
GET    /api/v1/matching/pathways/{id}
POST   /api/v1/matching/feedback
PUT    /api/v1/matching/preferences
```

**Program Catalog Endpoints:**
```
GET    /api/v1/programs
GET    /api/v1/programs/search
GET    /api/v1/programs/{id}
GET    /api/v1/programs/categories
GET    /api/v1/programs/providers

POST   /api/v1/programs (admin)
PUT    /api/v1/programs/{id} (admin)
DELETE /api/v1/programs/{id} (admin)
```

**Job Service Endpoints:**
```
GET    /api/v1/jobs
GET    /api/v1/jobs/search
GET    /api/v1/jobs/{id}
POST   /api/v1/jobs/apply
GET    /api/v1/jobs/applications
GET    /api/v1/jobs/applications/{id}
PUT    /api/v1/jobs/applications/{id}/status
```

**Barrier Navigation Endpoints:**
```
POST   /api/v1/barriers/assess
GET    /api/v1/barriers/programs
GET    /api/v1/barriers/programs/{id}
POST   /api/v1/barriers/applications
GET    /api/v1/barriers/applications
GET    /api/v1/barriers/applications/{id}/status
```

**Integration Service Endpoints:**
```
POST   /api/v1/integrations/kansasworks/sync
POST   /api/v1/integrations/wsutech/sync
POST   /api/v1/integrations/butlercc/sync
POST   /api/v1/webhooks/partner/{partnerId}
GET    /api/v1/integrations/status
```

### 4.3 Authentication & Authorization

**Authentication Flow:**
1. User enters credentials
2. User Service validates against PostgreSQL
3. User Service generates JWT token (expires in 24 hours)
4. JWT contains: userId, email, role, permissions
5. Frontend stores JWT in httpOnly cookie (secure)
6. Frontend includes JWT in Authorization header for API calls
7. API Gateway validates JWT on every request
8. Refresh token flow for long-lived sessions

**Authorization Roles:**
- **User:** Standard job seeker
- **Employer:** Can post jobs and view applicants
- **TrainingProvider:** Can manage program catalog
- **WorkforceCenter:** Can view users and assist with enrollment
- **Admin:** Full system access

**Permission Model:**
```json
{
  "user": ["read:own-profile", "write:own-profile", "apply:jobs", "enroll:programs"],
  "employer": ["read:jobs", "write:jobs", "read:applicants"],
  "trainingProvider": ["read:programs", "write:programs", "read:enrollments"],
  "workforceCenter": ["read:users", "assist:enrollment", "read:analytics"],
  "admin": ["*"]
}
```

### 4.4 Error Handling

**Standard Error Response:**
```json
{
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "Invalid input data",
    "details": [
      {
        "field": "email",
        "message": "Invalid email format"
      }
    ],
    "requestId": "req_abc123xyz",
    "timestamp": "2025-10-25T12:34:56Z"
  }
}
```

**Error Codes:**
- 400: Bad Request (validation errors)
- 401: Unauthorized (authentication required)
- 403: Forbidden (insufficient permissions)
- 404: Not Found
- 409: Conflict (duplicate resource)
- 429: Too Many Requests (rate limit exceeded)
- 500: Internal Server Error
- 503: Service Unavailable (maintenance or overload)

**Error Monitoring:**
- All errors logged to CloudWatch
- Critical errors sent to Sentry
- Error rates monitored with alerts
- PagerDuty integration for on-call

---

## 5. AI/ML Pipeline

### 5.1 Pathway Matching Model

**Problem Statement:**
Given a user's skills, interests, constraints, and location, recommend the top 3-5 career pathways (training program + job outcome combinations) that maximize likelihood of success and satisfaction.

**Model Architecture:**
Hybrid recommendation system combining:
1. **Collaborative Filtering:** "Users like you succeeded with these pathways"
2. **Content-Based Filtering:** "Pathways that match your skills and interests"
3. **Constraint Satisfaction:** Filter pathways that violate user constraints

**Input Features:**

**User Features:**
- `skills`: List of current skills (encoded as multi-hot vector)
- `skill_levels`: Proficiency levels (beginner/intermediate/advanced)
- `interests`: Career interest categories (Holland Codes: RIASEC)
- `education_level`: Highest degree completed
- `work_experience_years`: Years of work experience
- `location`: County/city
- `time_availability`: Hours per week available
- `financial_constraints`: Max out-of-pocket cost
- `transportation_access`: Boolean or categorical
- `childcare_needs`: Boolean
- `digital_literacy`: Self-assessed level

**Program Features:**
- `required_skills`: Prerequisites
- `duration_weeks`: Program length
- `cost`: Tuition and fees
- `schedule_type`: Full-time, part-time, evening, online
- `location`: County/city
- `credential_type`: Certificate, associate, bachelor, etc.
- `historical_completion_rate`: % who complete
- `historical_placement_rate`: % who get jobs
- `average_salary`: Post-program earnings

**Job Features:**
- `required_credential`: What the program provides
- `demand_score`: Number of openings / applicants
- `growth_rate`: Projected job growth
- `median_salary`: Expected earnings

**Model Training Data:**
- Historical user pathways (who enrolled where, who succeeded)
- Job placement outcomes
- User feedback on recommendations
- Skills taxonomies (O*NET, Burning Glass)
- Labor market data (Kansas Labor Information Center)

**Model Training Process:**
1. **Data Collection:** Gather historical data from pilot + partner data
2. **Feature Engineering:**
   - Encode categorical variables (one-hot, target encoding)
   - Normalize numerical features
   - Create interaction features (skill × program type)
3. **Train/Test Split:** 80/20 split, stratified by outcome
4. **Model Training:**
   - Train collaborative filtering model (matrix factorization or neural collaborative filtering)
   - Train content-based model (gradient boosting or neural network)
   - Tune hyperparameters with cross-validation
5. **Model Evaluation:**
   - Precision@K: Are top recommendations relevant?
   - Recall@K: Do we capture all good pathways?
   - NDCG: Ranking quality
   - Diversity: Avoid filter bubbles
6. **Model Deployment:**
   - Export model to TensorFlow SavedModel format
   - Deploy to TensorFlow Serving or FastAPI endpoint
   - A/B test new model vs. current model

**Inference Process:**
1. User completes assessment
2. User Service calls Matching Service API
3. Matching Service:
   - Fetches user features from database
   - Fetches all programs from Program Catalog
   - Runs collaborative filtering model → scores
   - Runs content-based model → scores
   - Combines scores (weighted average or meta-model)
   - Applies constraint filters
   - Ranks pathways by final score
   - Returns top 5 recommendations
4. Response includes:
   - Pathway details (program + expected job)
   - Match score (0-100)
   - Explanation (why recommended)
   - Success probability estimate
   - Timeline to employment
   - Total cost and financial assistance options

**Model Monitoring:**
- Prediction latency (target: <500ms)
- Recommendation acceptance rate
- Enrollment conversion rate
- Feedback scores (thumbs up/down)
- Model drift detection (feature distributions)
- Retrain model monthly with new data

### 5.2 Skills Extraction Model

**Purpose:** Extract structured skills from unstructured text (resumes, job descriptions)

**Approach:**
- Named Entity Recognition (NER) with pre-trained BERT model fine-tuned on skills
- Skills taxonomy mapping (O*NET, Burning Glass)
- Confidence scoring for each extracted skill

**Technology:**
- Hugging Face Transformers (BERT/RoBERTa)
- spaCy for NER pipeline
- Custom post-processing for taxonomy mapping

### 5.3 Job-Program Matching Model

**Purpose:** Match training programs to job openings based on credential requirements

**Approach:**
- Rule-based system with manual mappings (e.g., "Certified Medical Assistant" → healthcare jobs)
- Text similarity between program description and job description (TF-IDF or embeddings)
- Learning-to-rank model trained on successful placements

**Technology:**
- Sentence-BERT for semantic similarity
- LambdaMART or RankNet for learning-to-rank

### 5.4 Outcome Prediction Model

**Purpose:** Predict likelihood of user completing a program and getting a job

**Approach:**
- Classification model (logistic regression or gradient boosting)
- Features: user profile, program characteristics, historical success rates
- Output: Probability of success (0-1)

**Use Case:**
- Show users realistic expectations
- Prioritize users needing additional support
- Measure ROI for stakeholders

---

## 6. Integration Architecture

### 6.1 Partner Integration Patterns

**Pattern 1: REST API Integration (Preferred)**
- Training provider exposes REST API
- PathwayKS calls API for real-time data
- OAuth 2.0 authentication
- Rate limiting and retry logic
- Example: WSU Tech API, Butler CC API

**Pattern 2: Webhook Integration**
- Partner sends event notifications to PathwayKS
- PathwayKS exposes webhook endpoint
- Validates webhook signature for security
- Processes event and updates database
- Example: Employer ATS sends "application status changed" event

**Pattern 3: Batch File Transfer**
- Partner generates daily/weekly data file (CSV, JSON, XML)
- PathwayKS retrieves via SFTP or S3
- Processes file and updates database
- Example: KansasWorks job listing export

**Pattern 4: Web Scraping (Last Resort)**
- When no API or file transfer available
- PathwayKS scrapes partner website
- Respect robots.txt and rate limits
- Fragile (breaks when site changes)
- Example: Training providers without APIs

### 6.2 Integration Examples

**KansasWorks API Integration:**
```javascript
// Integration Service code
const axios = require('axios');

class KansasWorksClient {
  constructor(apiKey, baseURL) {
    this.apiKey = apiKey;
    this.baseURL = baseURL;
  }

  async getJobListings(filters = {}) {
    try {
      const response = await axios.get(`${this.baseURL}/api/jobs`, {
        params: filters,
        headers: {
          'Authorization': `Bearer ${this.apiKey}`,
          'Accept': 'application/json'
        },
        timeout: 10000
      });
      return response.data.jobs;
    } catch (error) {
      console.error('KansasWorks API error:', error);
      throw new Error('Failed to fetch job listings');
    }
  }

  async getTrainingPrograms(filters = {}) {
    try {
      const response = await axios.get(`${this.baseURL}/api/training`, {
        params: filters,
        headers: {
          'Authorization': `Bearer ${this.apiKey}`,
          'Accept': 'application/json'
        }
      });
      return response.data.programs;
    } catch (error) {
      console.error('KansasWorks API error:', error);
      throw new Error('Failed to fetch training programs');
    }
  }
}

module.exports = KansasWorksClient;
```

**WSU Tech Webhook Handler:**
```javascript
// Integration Service webhook endpoint
const express = require('express');
const crypto = require('crypto');

const router = express.Router();

// Verify webhook signature
function verifySignature(payload, signature, secret) {
  const hmac = crypto.createHmac('sha256', secret);
  const digest = hmac.update(payload).digest('hex');
  return crypto.timingSafeEqual(
    Buffer.from(signature),
    Buffer.from(digest)
  );
}

// Webhook endpoint
router.post('/webhooks/wsutech', async (req, res) => {
  const signature = req.headers['x-wsutech-signature'];
  const payload = JSON.stringify(req.body);

  // Verify signature
  if (!verifySignature(payload, signature, process.env.WSUTECH_SECRET)) {
    return res.status(401).json({ error: 'Invalid signature' });
  }

  // Process event
  const { event_type, data } = req.body;

  switch (event_type) {
    case 'enrollment.completed':
      await handleEnrollmentCompleted(data);
      break;
    case 'program.updated':
      await handleProgramUpdated(data);
      break;
    default:
      console.log('Unknown event type:', event_type);
  }

  res.status(200).json({ received: true });
});

async function handleEnrollmentCompleted(data) {
  // Update user record
  const { user_id, program_id, enrollment_date } = data;
  await db.users.update(
    { id: user_id },
    { enrolled_program: program_id, enrollment_date }
  );
  // Send notification
  await notificationService.sendEmail(
    user_id,
    'Enrollment Confirmed',
    `You're enrolled in ${program_id}`
  );
}

async function handleProgramUpdated(data) {
  // Update program catalog
  const { program_id, updates } = data;
  await db.programs.update({ id: program_id }, updates);
}

module.exports = router;
```

### 6.3 Data Synchronization Strategy

**Real-Time Sync (API-based):**
- Job listings: Sync every 4 hours
- Program availability: Sync every 24 hours
- User applications: Real-time

**Batch Sync (File-based):**
- Historical placement data: Weekly
- Labor market statistics: Monthly
- Partner directory: Monthly

**Event-Driven Sync (Webhook-based):**
- Enrollment status: Real-time
- Application status: Real-time
- Program changes: Real-time

**Conflict Resolution:**
- Last-write-wins for most data
- Manual review for critical data (e.g., program cost changes)
- Audit log for all data changes

---

## 7. Data Models

### 7.1 PostgreSQL Schema (User Data)

**Users Table:**
```sql
CREATE TABLE users (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  email VARCHAR(255) UNIQUE NOT NULL,
  password_hash VARCHAR(255) NOT NULL,
  first_name VARCHAR(100) NOT NULL,
  last_name VARCHAR(100) NOT NULL,
  phone VARCHAR(20),
  date_of_birth DATE,
  location_county VARCHAR(100),
  location_city VARCHAR(100),
  education_level VARCHAR(50),
  work_experience_years INT,
  time_availability_hours_per_week INT,
  financial_constraints_max_cost DECIMAL(10, 2),
  transportation_access BOOLEAN,
  childcare_needs BOOLEAN,
  digital_literacy_level VARCHAR(20),
  role VARCHAR(20) DEFAULT 'user',
  status VARCHAR(20) DEFAULT 'active',
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE INDEX idx_users_email ON users(email);
CREATE INDEX idx_users_location ON users(location_county, location_city);
CREATE INDEX idx_users_status ON users(status);
```

**User Skills Table:**
```sql
CREATE TABLE user_skills (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID REFERENCES users(id) ON DELETE CASCADE,
  skill_name VARCHAR(100) NOT NULL,
  skill_level VARCHAR(20), -- beginner, intermediate, advanced
  years_experience INT,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE INDEX idx_user_skills_user_id ON user_skills(user_id);
CREATE INDEX idx_user_skills_skill_name ON user_skills(skill_name);
```

**User Interests Table:**
```sql
CREATE TABLE user_interests (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID REFERENCES users(id) ON DELETE CASCADE,
  interest_category VARCHAR(50) NOT NULL, -- RIASEC codes
  interest_score INT, -- 1-10
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE INDEX idx_user_interests_user_id ON user_interests(user_id);
```

**Pathways Table:**
```sql
CREATE TABLE pathways (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID REFERENCES users(id) ON DELETE CASCADE,
  program_id VARCHAR(100) NOT NULL,
  match_score DECIMAL(5, 2),
  rank INT,
  selected BOOLEAN DEFAULT FALSE,
  feedback VARCHAR(20), -- thumbs_up, thumbs_down, null
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE INDEX idx_pathways_user_id ON pathways(user_id);
CREATE INDEX idx_pathways_program_id ON pathways(program_id);
```

**Enrollments Table:**
```sql
CREATE TABLE enrollments (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID REFERENCES users(id) ON DELETE CASCADE,
  program_id VARCHAR(100) NOT NULL,
  provider_id VARCHAR(100) NOT NULL,
  enrollment_date DATE NOT NULL,
  expected_completion_date DATE,
  actual_completion_date DATE,
  status VARCHAR(20), -- enrolled, in_progress, completed, dropped
  credential_earned VARCHAR(255),
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE INDEX idx_enrollments_user_id ON enrollments(user_id);
CREATE INDEX idx_enrollments_status ON enrollments(status);
```

**Job Applications Table:**
```sql
CREATE TABLE job_applications (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID REFERENCES users(id) ON DELETE CASCADE,
  job_id VARCHAR(100) NOT NULL,
  employer_id VARCHAR(100) NOT NULL,
  application_date DATE NOT NULL,
  status VARCHAR(20), -- submitted, under_review, interview_scheduled, offer, rejected, accepted
  interview_date TIMESTAMP,
  offer_salary DECIMAL(10, 2),
  offer_accepted BOOLEAN,
  start_date DATE,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE INDEX idx_job_applications_user_id ON job_applications(user_id);
CREATE INDEX idx_job_applications_job_id ON job_applications(job_id);
CREATE INDEX idx_job_applications_status ON job_applications(status);
```

**Placements Table:**
```sql
CREATE TABLE placements (
  id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
  user_id UUID REFERENCES users(id) ON DELETE CASCADE,
  enrollment_id UUID REFERENCES enrollments(id),
  job_application_id UUID REFERENCES job_applications(id),
  employer_id VARCHAR(100) NOT NULL,
  job_title VARCHAR(255) NOT NULL,
  start_date DATE NOT NULL,
  end_date DATE,
  starting_salary DECIMAL(10, 2),
  still_employed BOOLEAN DEFAULT TRUE,
  retention_90_day BOOLEAN,
  retention_180_day BOOLEAN,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE INDEX idx_placements_user_id ON placements(user_id);
CREATE INDEX idx_placements_employer_id ON placements(employer_id);
```

### 7.2 MongoDB Schema (Program Catalog)

**Programs Collection:**
```json
{
  "_id": "wsutech_unmanned_aircraft_systems",
  "provider_id": "wsutech",
  "provider_name": "WSU Tech",
  "name": "Unmanned Aircraft Systems",
  "description": "Training for FAA Part 107 Remote Pilot Certificate...",
  "category": "Aviation",
  "subcategory": "Drones & UAS",
  "duration_weeks": 16,
  "schedule_type": "part-time",
  "schedule_details": "Evenings, 6-9pm, Mon-Wed",
  "location": {
    "county": "Sedgwick",
    "city": "Wichita",
    "address": "4004 N. Webb Road",
    "online_option": true
  },
  "cost": {
    "tuition": 0,
    "fees": 250,
    "books": 150,
    "total": 400,
    "financial_aid_available": true,
    "wichita_promise_eligible": true
  },
  "prerequisites": {
    "education": "high_school_diploma",
    "skills": [],
    "experience": "none"
  },
  "outcomes": {
    "credential": "FAA Part 107 Remote Pilot Certificate",
    "historical_completion_rate": 0.85,
    "historical_placement_rate": 0.78,
    "average_time_to_employment_days": 45,
    "median_starting_salary": 45000
  },
  "target_jobs": [
    "Drone Pilot",
    "UAS Technician",
    "Aerial Photographer",
    "UAS Inspector"
  ],
  "start_dates": ["2025-01-15", "2025-04-01", "2025-08-15"],
  "enrollment_url": "https://wsutech.edu/unmanned-aircraft-systems/apply",
  "contact": {
    "phone": "316-677-9400",
    "email": "admissions@wsutech.edu"
  },
  "created_at": "2025-01-01T00:00:00Z",
  "updated_at": "2025-10-01T00:00:00Z",
  "data_source": "wsutech_api",
  "last_synced": "2025-10-25T08:00:00Z"
}
```

**Jobs Collection:**
```json
{
  "_id": "spirit_aero_machinist_2025_001",
  "employer_id": "spirit_aerosystems",
  "employer_name": "Spirit AeroSystems",
  "title": "CNC Machinist",
  "description": "Operate CNC machines to manufacture aerospace components...",
  "category": "Manufacturing",
  "subcategory": "Machining",
  "location": {
    "county": "Sedgwick",
    "city": "Wichita",
    "address": "3801 S. Oliver",
    "remote_option": false
  },
  "employment_type": "full-time",
  "schedule": "1st shift, 6am-2:30pm",
  "salary": {
    "min": 45000,
    "max": 65000,
    "currency": "USD",
    "period": "annual"
  },
  "requirements": {
    "education": "high_school_diploma",
    "credentials": ["CNC Machining Certificate"],
    "experience_years": 1,
    "skills": ["CNC Programming", "Blueprint Reading", "Precision Measurement"]
  },
  "benefits": [
    "Health Insurance",
    "401(k) Match",
    "Tuition Reimbursement",
    "Paid Time Off"
  ],
  "posted_date": "2025-10-15",
  "expiration_date": "2025-12-15",
  "application_url": "https://careers.spiritaero.com/job/12345",
  "pathwayks_guaranteed_interview": true,
  "created_at": "2025-10-15T00:00:00Z",
  "updated_at": "2025-10-20T00:00:00Z",
  "data_source": "spirit_ats_api",
  "last_synced": "2025-10-25T06:00:00Z"
}
```

**Partners Collection:**
```json
{
  "_id": "wsutech",
  "name": "WSU Tech",
  "type": "training_provider",
  "description": "Technical college offering workforce training...",
  "website": "https://wsutech.edu",
  "location": {
    "county": "Sedgwick",
    "city": "Wichita",
    "address": "4004 N. Webb Road, Wichita, KS 67226"
  },
  "contact": {
    "phone": "316-677-9400",
    "email": "info@wsutech.edu"
  },
  "integration": {
    "type": "api",
    "api_base_url": "https://api.wsutech.edu/v1",
    "auth_type": "oauth2",
    "webhook_url": "https://api.pathwayks.org/webhooks/wsutech",
    "sync_schedule": "daily_8am"
  },
  "statistics": {
    "total_programs": 45,
    "total_enrollments_via_pathwayks": 327,
    "average_completion_rate": 0.82
  },
  "partnership_start_date": "2025-01-01",
  "status": "active",
  "created_at": "2025-01-01T00:00:00Z",
  "updated_at": "2025-10-20T00:00:00Z"
}
```

---

## 8. Security & Compliance

### 8.1 Security Architecture

**Defense in Depth:**
1. **Network Security:**
   - VPC with public and private subnets
   - Security groups (firewall rules)
   - AWS WAF (web application firewall)
   - DDoS protection (AWS Shield)

2. **Application Security:**
   - Input validation on all user inputs
   - Output encoding to prevent XSS
   - Parameterized queries to prevent SQL injection
   - CSRF tokens on state-changing requests
   - Rate limiting to prevent abuse

3. **Authentication & Authorization:**
   - Multi-factor authentication (MFA) for admin users
   - JWT tokens with short expiration (24 hours)
   - Refresh token rotation
   - Role-based access control (RBAC)
   - Principle of least privilege

4. **Data Security:**
   - Encryption at rest (AES-256)
   - Encryption in transit (TLS 1.3)
   - Database encryption (RDS encryption)
   - Secrets management (AWS Secrets Manager)
   - PII data masking in logs

5. **API Security:**
   - API key authentication for partner APIs
   - OAuth 2.0 for user-delegated access
   - API rate limiting (per user, per IP)
   - Request signature verification for webhooks

### 8.2 Compliance Requirements

**FERPA (Family Educational Rights and Privacy Act):**
- Protects education records
- Requires consent for data sharing
- PathwayKS compliance:
  - User consent during registration
  - Data sharing agreements with training providers
  - Audit logs for all data access
  - Parental consent for users under 18

**SOC 2 Type II:**
- Security, availability, confidentiality, processing integrity, privacy
- Annual audit by independent CPA firm
- PathwayKS preparations:
  - Security policies and procedures documented
  - Access controls implemented
  - Monitoring and logging in place
  - Incident response plan
  - Business continuity plan

**WCAG 2.1 Level AA (Accessibility):**
- Ensures access for users with disabilities
- PathwayKS compliance:
  - Semantic HTML
  - Keyboard navigation
  - Screen reader support
  - Color contrast ratios (4.5:1 minimum)
  - Alt text for images
  - Captions for videos

**GDPR (General Data Protection Regulation):**
- Even though Kansas-focused, some users may be EU residents
- PathwayKS compliance:
  - Privacy policy and terms of service
  - Cookie consent banner
  - Data export functionality
  - Data deletion functionality
  - Data processing agreements with partners

### 8.3 Penetration Testing

**Annual Penetration Tests:**
- Conducted by third-party security firm
- OWASP Top 10 coverage
- Social engineering tests
- Network security tests
- Remediation within 30 days of findings

**Continuous Vulnerability Scanning:**
- Automated scans with Snyk
- Dependency vulnerability checks
- Container image scanning
- Infrastructure vulnerability scanning

---

## 9. Deployment & Infrastructure

### 9.1 AWS Infrastructure

**Compute:**
- ECS Fargate for containerized services (auto-scaling)
- Lambda for event-driven functions (webhooks, scheduled tasks)
- EC2 for ML training (GPU instances, spot instances for cost savings)

**Storage:**
- RDS PostgreSQL (Multi-AZ for high availability)
- DocumentDB (MongoDB-compatible, managed service)
- ElastiCache Redis (cluster mode enabled)
- S3 (data files, backups, static assets)

**Networking:**
- VPC with public and private subnets
- Application Load Balancer (ALB) for HTTP/HTTPS traffic
- CloudFront CDN for static assets and API caching
- Route 53 for DNS

**Monitoring:**
- CloudWatch for metrics, logs, and alarms
- X-Ray for distributed tracing
- SNS for alerts (email, SMS, PagerDuty)

**Security:**
- IAM roles and policies (least privilege)
- Secrets Manager for API keys and passwords
- KMS for encryption keys
- WAF for web application security
- GuardDuty for threat detection

### 9.2 CI/CD Pipeline

**Source Control:**
- GitHub for code hosting
- Protected main branch (requires pull request + approvals)
- Branch naming convention: feature/, bugfix/, hotfix/

**Continuous Integration:**
1. Developer pushes code to feature branch
2. GitHub Actions workflow triggers:
   - Lint code (ESLint, Pylint)
   - Run unit tests (Jest, Pytest)
   - Run integration tests
   - Build Docker images
   - Scan for vulnerabilities (Snyk)
3. Pull request review and approval
4. Merge to main branch

**Continuous Deployment:**
1. Merge to main triggers deployment workflow
2. Build and tag Docker images
3. Push images to AWS ECR (Elastic Container Registry)
4. Update ECS task definitions
5. Deploy to staging environment
6. Run smoke tests
7. Manual approval for production deployment
8. Deploy to production with blue/green deployment
9. Monitor metrics and rollback if issues detected

**Deployment Environments:**
- **Development:** Developer local environments (Docker Compose)
- **Staging:** AWS environment matching production (for testing)
- **Production:** AWS environment serving end users

### 9.3 Infrastructure as Code

**Terraform Configuration Example:**
```hcl
# VPC
resource "aws_vpc" "main" {
  cidr_block           = "10.0.0.0/16"
  enable_dns_hostnames = true
  tags = {
    Name = "pathwayks-vpc"
  }
}

# Public Subnets
resource "aws_subnet" "public_a" {
  vpc_id                  = aws_vpc.main.id
  cidr_block              = "10.0.1.0/24"
  availability_zone       = "us-gov-west-1a"
  map_public_ip_on_launch = true
  tags = {
    Name = "pathwayks-public-a"
  }
}

resource "aws_subnet" "public_b" {
  vpc_id                  = aws_vpc.main.id
  cidr_block              = "10.0.2.0/24"
  availability_zone       = "us-gov-west-1b"
  map_public_ip_on_launch = true
  tags = {
    Name = "pathwayks-public-b"
  }
}

# Private Subnets
resource "aws_subnet" "private_a" {
  vpc_id            = aws_vpc.main.id
  cidr_block        = "10.0.11.0/24"
  availability_zone = "us-gov-west-1a"
  tags = {
    Name = "pathwayks-private-a"
  }
}

resource "aws_subnet" "private_b" {
  vpc_id            = aws_vpc.main.id
  cidr_block        = "10.0.12.0/24"
  availability_zone = "us-gov-west-1b"
  tags = {
    Name = "pathwayks-private-b"
  }
}

# RDS PostgreSQL
resource "aws_db_instance" "main" {
  identifier              = "pathwayks-postgres"
  engine                  = "postgres"
  engine_version          = "15.3"
  instance_class          = "db.t3.medium"
  allocated_storage       = 100
  storage_type            = "gp3"
  storage_encrypted       = true
  db_name                 = "pathwayks"
  username                = var.db_username
  password                = var.db_password
  multi_az                = true
  publicly_accessible     = false
  vpc_security_group_ids  = [aws_security_group.rds.id]
  db_subnet_group_name    = aws_db_subnet_group.main.name
  backup_retention_period = 30
  skip_final_snapshot     = false
  final_snapshot_identifier = "pathwayks-final-snapshot"
  tags = {
    Name = "pathwayks-postgres"
  }
}

# ECS Cluster
resource "aws_ecs_cluster" "main" {
  name = "pathwayks-cluster"
  setting {
    name  = "containerInsights"
    value = "enabled"
  }
  tags = {
    Name = "pathwayks-cluster"
  }
}

# ECS Task Definition (User Service)
resource "aws_ecs_task_definition" "user_service" {
  family                   = "pathwayks-user-service"
  network_mode             = "awsvpc"
  requires_compatibilities = ["FARGATE"]
  cpu                      = "512"
  memory                   = "1024"
  execution_role_arn       = aws_iam_role.ecs_execution_role.arn
  task_role_arn            = aws_iam_role.ecs_task_role.arn

  container_definitions = jsonencode([{
    name      = "user-service"
    image     = "${aws_ecr_repository.user_service.repository_url}:latest"
    essential = true
    portMappings = [{
      containerPort = 3000
      protocol      = "tcp"
    }]
    environment = [
      {
        name  = "NODE_ENV"
        value = "production"
      },
      {
        name  = "DB_HOST"
        value = aws_db_instance.main.address
      }
    ]
    secrets = [
      {
        name      = "DB_PASSWORD"
        valueFrom = aws_secretsmanager_secret.db_password.arn
      }
    ]
    logConfiguration = {
      logDriver = "awslogs"
      options = {
        "awslogs-group"         = "/ecs/pathwayks-user-service"
        "awslogs-region"        = "us-gov-west-1"
        "awslogs-stream-prefix" = "ecs"
      }
    }
  }])
}

# ECS Service (User Service)
resource "aws_ecs_service" "user_service" {
  name            = "pathwayks-user-service"
  cluster         = aws_ecs_cluster.main.id
  task_definition = aws_ecs_task_definition.user_service.arn
  desired_count   = 2
  launch_type     = "FARGATE"

  network_configuration {
    subnets          = [aws_subnet.private_a.id, aws_subnet.private_b.id]
    security_groups  = [aws_security_group.ecs_tasks.id]
    assign_public_ip = false
  }

  load_balancer {
    target_group_arn = aws_lb_target_group.user_service.arn
    container_name   = "user-service"
    container_port   = 3000
  }

  depends_on = [aws_lb_listener.main]
}

# Application Load Balancer
resource "aws_lb" "main" {
  name               = "pathwayks-alb"
  internal           = false
  load_balancer_type = "application"
  security_groups    = [aws_security_group.alb.id]
  subnets            = [aws_subnet.public_a.id, aws_subnet.public_b.id]
  tags = {
    Name = "pathwayks-alb"
  }
}

# ... (additional resources: target groups, listeners, security groups, etc.)
```

---

## 10. Development Workflow

### 10.1 Agile Methodology

**Sprint Structure:**
- 2-week sprints
- Sprint planning (Monday Week 1, 2 hours)
- Daily standups (15 minutes)
- Sprint review (Friday Week 2, 1 hour)
- Sprint retrospective (Friday Week 2, 1 hour)

**Team Roles:**
- Product Owner: Prioritizes backlog, defines user stories
- Scrum Master: Facilitates ceremonies, removes blockers
- Development Team: Engineers, designers, QA

**Tools:**
- GitHub Projects for sprint board
- GitHub Issues for user stories and tasks
- Slack for daily communication
- Zoom for meetings

### 10.2 Code Review Process

**Pull Request Requirements:**
1. All tests pass (unit + integration)
2. Code coverage ≥ 80%
3. Linting passes (no errors)
4. At least 1 approval from team member
5. No merge conflicts
6. Pull request template filled out:
   - Description of changes
   - Related issue number
   - Screenshots (if UI change)
   - Testing steps
   - Deployment notes

**Code Review Checklist:**
- Code is readable and maintainable
- Follows coding standards
- No security vulnerabilities
- Error handling is appropriate
- Tests cover edge cases
- Documentation updated (if needed)

### 10.3 Testing Strategy

**Unit Tests:**
- Coverage target: 80%+
- Frameworks: Jest (JavaScript), Pytest (Python)
- Run on every commit
- Fast execution (<5 minutes)

**Integration Tests:**
- Test service-to-service communication
- Test database interactions
- Test external API integrations (mocked)
- Run on every pull request
- Moderate execution time (10-20 minutes)

**End-to-End Tests:**
- Test critical user flows:
  - User registration and assessment
  - Pathway recommendation
  - Program enrollment
  - Job application
- Framework: Cypress
- Run nightly and before production deployments
- Longer execution time (30-60 minutes)

**Load Tests:**
- Simulate high traffic scenarios
- Framework: k6
- Metrics: requests/second, latency, error rate
- Run before major releases
- Performance targets:
  - API response time <500ms (p95)
  - Support 10,000 concurrent users
  - Throughput: 1,000 requests/second

### 10.4 Documentation Standards

**Code Documentation:**
- JSDoc comments for JavaScript/TypeScript functions
- Docstrings for Python functions
- README.md in every repository
- Architecture Decision Records (ADRs) for major decisions

**API Documentation:**
- OpenAPI 3.0 specifications
- Example requests and responses
- Error code documentation
- Hosted on Redoc or Swagger UI

**User Documentation:**
- User guide (how to use PathwayKS)
- FAQ section
- Video tutorials for key workflows
- Hosted on Docusaurus site

---

## 11. Scalability & Performance

### 11.1 Scalability Strategy

**Horizontal Scaling:**
- Stateless services enable easy horizontal scaling
- ECS/Fargate auto-scaling based on CPU/memory utilization
- Database read replicas for read-heavy workloads
- Elasticsearch cluster with multiple nodes

**Vertical Scaling:**
- Initial instance sizes: t3.medium
- Upgrade to larger instances as needed
- Monitor resource utilization and right-size instances

**Caching Strategy:**
- Redis caching for frequently accessed data:
  - User sessions (TTL: 24 hours)
  - Program catalog (TTL: 1 hour, invalidate on update)
  - API responses (TTL: 5 minutes for search results)
- CDN caching for static assets (TTL: 7 days)
- Browser caching for JS/CSS bundles

**Database Optimization:**
- Indexing on frequently queried columns
- Query optimization (EXPLAIN ANALYZE)
- Connection pooling to reduce overhead
- Materialized views for complex analytics queries
- Partitioning for large tables (e.g., audit logs by month)

### 11.2 Performance Targets

**Response Time:**
- API endpoints: <500ms (p95)
- Page load time: <2 seconds (p95)
- AI model inference: <500ms

**Availability:**
- Uptime SLA: 99.9% (43 minutes/month downtime)
- Multi-AZ deployment for high availability
- Auto-failover for database

**Throughput:**
- Support 10,000 concurrent users
- 1,000 requests/second API throughput
- 100 pathway recommendations/second

**Data Freshness:**
- Job listings: 4-hour sync
- Program catalog: 24-hour sync
- Real-time for user actions (enrollment, application)

### 11.3 Monitoring & Alerting

**Key Metrics:**
- Application metrics:
  - Request rate, error rate, response time
  - User registrations, pathway recommendations, enrollments, placements
- Infrastructure metrics:
  - CPU utilization, memory utilization, disk I/O
  - Network throughput
- Business metrics:
  - Conversion funnel (registration → enrollment → placement)
  - User engagement (DAU, MAU, session duration)

**Alerts:**
- Critical: Error rate >5% (PagerDuty)
- Warning: Response time >1s (Slack)
- Info: Daily summary report (Email)

**Dashboards:**
- Real-time operational dashboard (Datadog)
- Business metrics dashboard (internal admin panel)
- Partner performance dashboard (visible to partners)

---

## 12. Implementation Roadmap

### 12.1 Phase 1: MVP (Months 1-3)

**Month 1: Foundation**
- Team assembly and onboarding
- Development environment setup
- GitHub repository structure
- AWS infrastructure provisioning (Terraform)
- Database schema design and implementation
- API specification (OpenAPI)
- Frontend scaffolding (Next.js)
- Partner agreements (Workforce Alliance, WSU Tech, KansasWorks Wichita)

**Month 2: Core Features**
- User registration and authentication
- Skills assessment module
- Program catalog integration (WSU Tech, Butler CC)
- AI pathway matching engine (MVP version)
- Frontend UI components (React)
- User dashboard
- Unit tests and integration tests

**Month 3: Launch**
- Job listing integration (KansasWorks API)
- Barrier navigation tools
- Enrollment workflow
- Email notifications (AWS SES)
- Beta testing with 50 users
- Bug fixes and refinements
- Public launch in Sedgwick County
- Goal: 500 pilot users

**Key Deliverables:**
- Working MVP platform (web)
- 3 partner integrations
- 500 users registered
- 100+ pathway recommendations
- 50+ enrollments

### 12.2 Phase 2: Regional Expansion (Months 4-6)

**Month 4: Expansion Prep**
- Add Butler CC and Newman University APIs
- Expand program catalog to 100+ programs
- Refine AI matching model based on pilot data
- Mobile-responsive design improvements
- Analytics dashboard for partners
- Hire additional team members (5 FTE)

**Month 5: Regional Rollout**
- Launch in all 6 WASCK counties
- Activate regional workforce centers
- Employer partnership outreach
- First B2B contracts signed
- Enhanced search and filtering
- Coaching features

**Month 6: Optimization**
- A/B testing of features
- Performance optimization
- Advanced barrier navigation
- Mobile app development begins
- User feedback collection and iteration

**Key Deliverables:**
- 2,500 users across 6-county region
- 500+ enrollments
- 250+ job placements
- 3 employer partnerships
- 2 training provider SaaS subscriptions

### 12.3 Phase 3: Statewide Launch (Months 7-12)

**Month 7-8: Statewide Prep**
- Integrate all 27 KansasWorks centers
- Expand program catalog statewide (500+ programs)
- Kansas DOL contract finalization
- Statewide marketing campaign
- Mobile app beta (iOS + Android)

**Month 9-10: Statewide Rollout**
- Public launch with Kansas DOL endorsement
- Press releases and media coverage
- Digital advertising campaign
- Employer portal development
- Advanced analytics features

**Month 11-12: Scale & Optimize**
- Continuous feature enhancements
- Job matching algorithm improvements
- Partner feedback incorporation
- Year 2 planning
- Series A fundraising preparation

**Key Deliverables:**
- 10,000 users statewide
- 1,500+ enrollments (Year 1 total)
- 750+ job placements (Year 1 total)
- 10 employer partnerships
- 5 training provider subscriptions
- Mobile app launched (beta)

### 12.4 Year 2-3 Roadmap Highlights

**Year 2:**
- Scale to 25,000 users
- Advanced AI features (predictive success modeling, dynamic pathway adjustments)
- Employer talent management suite
- Career coaching video platform
- Expansion discussions with neighboring states
- Mobile app full launch (iOS + Android)

**Year 3:**
- 50,000+ users across Kansas and pilot states
- White-label platform for other state workforce agencies
- Advanced data analytics and insights products
- Integration with national job boards (Indeed, LinkedIn)
- Premium tier features for enterprises
- International expansion (if applicable)

---

## Conclusion

PathwayKS is designed as a modern, scalable, and secure platform to transform Kansas workforce development. The technology stack leverages industry-standard tools and best practices to deliver:

1. **User-Centric Experience:** Intuitive web and mobile apps that guide users from assessment to employment
2. **AI-Powered Matching:** Machine learning models that personalize pathway recommendations
3. **Seamless Integration:** API connections to partners for real-time data and automated enrollment
4. **Barrier Navigation:** Tools to identify and overcome transportation, childcare, and financial barriers
5. **Measurable Impact:** Comprehensive analytics to track outcomes and demonstrate ROI

The technical architecture supports rapid iteration, high availability, and future growth as PathwayKS scales from a pilot in Sedgwick County to statewide deployment and potential expansion to other states.

With a strong technical foundation, experienced team, and government partnership, PathwayKS is positioned to become the national model for workforce development platforms.

---

**Document Status:** Complete
**Next Review Date:** After Phase 1 completion (Month 3)
**Contact:** Technical Lead, PathwayKS Team

---
*End of Technical Walkthrough*
