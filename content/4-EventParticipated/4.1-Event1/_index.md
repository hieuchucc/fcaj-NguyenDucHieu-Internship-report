---
title: "Event 1"
date: 2026-05-09
weight: 1
chapter: false
pre: " <b> 4.1. </b> "
---


# Summary Report: “GenAI-powered App-DB Modernization workshop”

### Speakers
- **Nguyễn Tuấn Thịnh** - DevOps/Cloud Engineer


### Key Highlights

#### Why Prompt Engineering Matters

Ineffective communication with AI leads to several negative consequences:
- **Generic prompts → Generic outputs**: Fails to address specific domain or problem requirements.
- **Wasted tokens → Increased costs**: The model processes and outputs unnecessarily verbose text.
- **Ambiguous instructions**: Results in poor communication and misunderstandings.
- **Inconsistent results & Lost productivity**: Wastes valuable time through endless trial-and-error iterations.

#### Key Components of a Great Prompt

To build a high-performing prompt, clearly structure the following elements:
- **Role**: Who the model is pretending to be (e.g., Career coach for fresh graduates).
- **Instruction**: What the specific task is (e.g., Improve my internship self-introduction).
- **Context**: Relevant background information (e.g., DevOps Engineer with AWS, backend, and project experience).
- **Input Data**: The actual text to be analyzed or acted upon (e.g., "Hello, my name is Thinh...").
- **Output Format**: The desired structure, syntax, and style of the response.
- **Examples**: Few-shot demonstrations showing ideal inputs and outputs.
- **Constraints/Guidelines**: Clear boundaries on what to do or avoid (e.g., Under 80 words, simple, natural, clear, confident; do NOT include assumptions).

#### The Art of Communicating with AI & Token Economics

- **Golden Rules for Prompting**:
  - Be clear and specific; use directive language.
  - Use delimiters (e.g., Markdown tags, quotes, XML tags) to clearly separate sections.
  - Describe what Nshould be done (**DOs**) rather than what shouldn't (**DON'TS**).
  - Do not ask LLMs to perform complex mathematical calculations directly; allow "I Don't Know" responses to prevent hallucination.
  - Break long inputs into smaller, manageable segments.
- **Understanding Token Economics**:
  - Tokens are subword units (not always equivalent to whole words).
  - Token counts differ significantly across various languages.
  - *Cost Example (Claude Opus 4.6)*: Input tokens cost ~$5.00 / 1M tokens; Output tokens cost ~$25.00 / 1M tokens.

#### Advanced Prompting Techniques

- **Chain-of-Thought (CoT) Prompting**: Guiding the model to generate step-by-step reasoning before providing the final answer.
- **Self-Consistency**: Generating multiple reasoning paths (CoT) and selecting the most consistent or common answer.
- **Tree-of-Thoughts (ToT)**: Modeling reasoning as a tree structure, allowing the AI to explore, evaluate, and backtrack across different branches to find optimal solutions.
- **Retrieval-Augmented Generation (RAG) & Role Prompting**: Combining external knowledge retrieval with deep persona adoption for highly contextualized outputs.

#### Proptimizer Tool & AWS Serverless Architecture

**Proptimizer** is a browser extension that optimizes user prompts automatically and enables chatting with AI anywhere on the web.

- **Frontend & Content Delivery**:
  - **AWS CloudFront**: Global content delivery network (CDN) delivering web content with low latency and caching static assets.
  - **Amazon S3**: Scalable cloud storage for static website files, images, and backups with 99.999999999% durability.
- **Authentication & Security**:
  - **Amazon Cognito**: Manages user authentication/authorization, sign-up, sign-in, and JWT token generation.
- **API & Backend Logic**:
  - **Amazon API Gateway**: Routes API calls, manages traffic, handles rate limiting, and enforces authorization.
  - **AWS Lambda**: Serverless compute running backend code triggered on demand without managing servers.
- **AI Integration & Data Storage**:
  - **Amazon Bedrock**: Provides managed access to foundation AI models (Claude, GPT, etc.) to power the prompt optimization engine without requiring custom model training.
  - **Amazon DynamoDB**: NoSQL database for storing user data, prompts, and optimization history with millisecond response times and automatic scaling.
- **Monitoring & Operations**:
  - **Amazon CloudWatch Logs & Metrics**: Collects logs and tracks real-time system health metrics (API latency, error rates).
- **Operational Cost**: Built on a pure serverless architecture, achieving a baseline infrastructure cost of **$0** (excluding Amazon Bedrock model consumption fees).

---

### What Was Learned

#### Prompt Engineering Mindset

- **Core Principles**: Understanding why generic prompts fail and recognizing the crucial role of Context, Persona (Role), and Constraints in guiding LLM behavior.
- **Token Cost Management**: Gaining awareness of how LLMs calculate costs based on subword tokens and leveraging the price difference between input and output tokens to optimize budget.

#### LLM Communication Techniques

- Mastering the 6-component prompt structure: Role, Instruction, Context, Input, Output format, and Examples.
- Understanding and applying advanced reasoning models ranging from **Chain-of-Thought (CoT)** and **Self-Consistency** to **Tree-of-Thoughts (ToT)** for complex problem-solving.
- Improving response quality by utilizing directive language and framing instructions around positive actions (DOs) rather than negative restrictions (DON'TS).

#### Serverless Architecture for GenAI Applications

- Designing an end-to-end AI system integrated into a browser extension using an **AWS Serverless** blueprint.
- Achieving seamless integration between **Frontend (CloudFront/S3)**, **Authentication (Cognito)**, **Backend (API Gateway/Lambda)**, and **AI Engine (Amazon Bedrock)**.
- Understanding the economic advantages of serverless pricing models when deploying production-grade GenAI applications.

---

### Work Applications

- **Standardize Prompting Workflows**: Implement a structured prompting framework (Role - Task - Context - Constraints) across daily team operations to elevate AI output quality.
- **Apply CoT and ToT**: Utilize Chain-of-Thought and Tree-of-Thoughts reasoning when using AI for code debugging, architectural design, or multi-step technical analysis.
- **Optimize LLM Token Costs**: Audit existing LLM-integrated projects to control prompt lengths, eliminate redundant context, and reduce overall token consumption.
- **Build Serverless GenAI Architectures**: Reference the Proptimizer architecture as a blueprint to pilot internal microservices and tools powered by **AWS Lambda** and **Amazon Bedrock**.
- **Adopt Proptimizer**: Integrate browser-based automated prompt optimization tools into daily workflows to save time and streamline interactions with AI models.

---

### Event Experience (AWS First Cloud AI Journey)

Attending the **“Automated Prompt Engineering: Enhancing LLM Output Quality”** session by **Nguyen Tuan Thinh** at the AWS First Cloud AI Journey was an insightful experience that expanded my perspective on both AI utilization and cloud system design.

#### Learning from Practical Realities
- The presentation tackled real-world pain points directly: explaining why users frequently receive generic outputs from AI and demonstrating how to solve this systematically through structured engineering.
- The before-and-after comparison examples (such as the career coach self-introduction rewrite) were highly intuitive and easy to grasp.

#### The Synergy of Prompt Engineering and Cloud Architecture
- Going beyond simple "prompting tips," the speaker presented the actual AWS production architecture behind the **Proptimizer** project.
- It was inspiring to see how familiar AWS services (S3, CloudFront, Lambda, DynamoDB) integrate seamlessly with **Amazon Bedrock** to deliver a functional GenAI product with near-zero baseline infrastructure costs ($0 excluding model inference).

#### Key Takeaways
- Prompt engineering is an "art of communication" deeply grounded in scientific principles (modular structure, token management, reasoning frameworks).
- Automated Prompt Engineering is an inevitable step toward scaling productivity and ensuring consistent AI performance across enterprise environments.

#### Event Photos
![Event 1](/images/4-EventParticipated/event1.jpg)

> Overall, the session provided immense practical value, helping me not only communicate with AI more effectively but also learn an exemplary architectural pattern for building scalable AI products on the AWS cloud.