---
title: "Event 2"
date: 2026-05-23
weight: 1
chapter: false
pre: " <b> 4.2. </b> "
---

# Summary Report: “GenAI-powered App-DB Modernization workshop”

### Event Objectives

- Share best practices in modern application design and context engineering to optimize AI model performance.
- Introduce smart assistant solutions and Agentic AI capabilities to automate business workflows and eliminate repetitive tasks.
- Provide comprehensive Amazon CloudFront solutions to optimize CDN costs, strengthen security, and enhance network reliability and performance.
- Share the real-world journey of building a Neural Interface application (UTMorpho) from initial idea to reality under high-pressure Hackathon conditions.
- Analyze the technical root causes of non-determinism in Large Language Models (LLMs) and propose practical mitigation strategies.
- Introduce the Multi-Agent Paradigm designed to solve the financial data asymmetry issue in startup credit scoring for traditional banking systems.

### Speakers

- **Tinh Truong** - Platform Engineer, GoTymeX
- **Pham Nguyen Hai Anh** - G-AsiaPacific Vietnam, AWS Community Builder
- **Nguyen Tuan Thinh** - DevOps Engineer, First Cloud AI Journey
- LotusHacks 2026
- **Duc Dao** - Solution Architect, Cloud Kinetics
- **Vy Lam** - Senior Business Systems Analyst, VPBank 

### Key Highlights

#### Drawbacks and Negative Impacts of Legacy Frameworks

- **Flawed Prompting Approaches:** Users often lower AI efficiency by cramming raw data, repeating the obvious, or providing vague prompts.
- **Siloed and Scattered Data:** Businesses waste significant time and suffer productivity loss due to manual, repetitive workflows and dispersed data sources.
- **CDN Costs & Security Risks:** Enterprises face unpredictable spikes in CDN expenses and severe vulnerabilities to volumetric DDoS attacks.
- **The Illusion of Determinism in LLMs:** Blindly trusting that setting temperature = 0 will always yield a unique, consistent output is a critical mistake in production environments.
- **Financial Data Asymmetry:** Traditional banking frameworks frequently reject startup profiles due to a mismatch and lack of alignment in financial data models. 

#### Context Optimization & Generative AI Smart Assistants

- **Standard Context Application Framework:** Structuring system prompts based on 4 pillars: Goal, Relevant info, Constraints, and Success criteria.
- **The "Second AI Brain" Model:** Architecture for cloud-based cognitive systems leveraging AWS S3 and Amazon Bedrock.
- **Amazon Q Suite:** Intelligent assistant solutions that establish secure data connections (Bedrock, Databases, Web search) reinforced with Governance Guardrails. 

#### Infrastructure Optimization and Delivery via Amazon CloudFront

- **Edge-Level Defense Mechanisms:** Mitigating DDoS threats using AWS Shield, WAF, and protecting origin servers via Origin Cloaking (VPC/OAC).
- **Cost & Performance Optimization:** Transitioning to the new Fixed-Price Plans and implementing multi-tier caching architectures over HTTP/3.
- **Edge Logic Routing:** Executing automated data compression, Mutual TLS authentication, access control via Signed URLs, and edge logic handling with CloudFront Functions / Lambda@Edge.  

#### From Idea to Reality: The Hackathon Product Journey (UTMorpho)

- **Neural Interface Application:** UTMorpho allows users to seamlessly convert raw sketches into live frontend code using the Claude Sonnet 4 model.
- **High-Pressure Execution Workflows:** Managing the stress of a 36-hour sprint by strictly prioritizing goal-setting, core feature alignment, rapid integration, and final pitch preparation.

#### Unpacking LLM Non-Determinism

- **Technical Root Causes:** Understanding how non-associative floating-point operations on GPUs combined with inference batching by cloud providers create output variations.
- **Mitigation Frameworks:** Fine-tuning parameters to temperature = 0.1 to prevent word repetition, and deploying majority voting strategies across multiple runs.  

#### Enterprise-Grade Multi-Agent Architectures

- **Virtual Credit Committee:** Implementing a Multi-Agent system to evaluate startup risk from multiple dimensions, cutting down operational costs and processing times by over 95%.
- **Functional Decomposition:** Fragmenting AI responsibilities into specialized agents (Finance, Market, Team, Risk, Compliance) to ensure cross-checking and a balance of power. 

### Key Takeaways

#### Design Mindset

- **Context Quality > Context Quantity:** The structured relevance of context matters far more than the raw volume of data fed into an AI model.
- **Automation Flow Thinking:** Mastering the integration of diverse, cross-departmental data sources to drastically bridge the gap from analysis to action.
- **Edge Computing Mindset:** Prioritizing system resilience and high availability by defaulting to automated mechanisms like Origin Failover.
- **Embracing Probabilistic Nature:** Designing system logic to adapt to the inherent probability of LLMs instead of forcing a rigid, deterministic expectation.
- **Checks & Balances Paradigm:** Recognizing the constraints of a Single Agent (context limits, diluted expertise) to transition toward Multi-Agent harmony.

#### Technical Architecture

- Developing a solid foundation in Context Engineering system design.
- Navigating Agentic AI mechanics alongside critical corporate policies on Data Governance & Security.
- Enforcing structural outputs using configuration parameters (JSON mode, regex grammars) instead of relying solely on natural language instructions.
- Architecting a three-layer Guardrails framework (Input, Processing, Output) to filter malicious content and protect sensitive corporate data.
- Troubleshooting technical AI hurdles: preventing AI Overgeneration and managing strict Token Limits under tight deadlines. 

#### Modernization Strategy

- **Phased approach**: No rushing — follow a clear roadmap  
- **7Rs framework**: Multiple modernization paths depending on the application  
- **ROI measurement**: Cost reduction + business agility  

### Applying to Work

- Deploy the Standard Context Framework (Goal, Relevant info, Constraints, Success criteria) to overhaul system prompt configurations for current AI projects.
- Evaluate Amazon Q Suite Integration to automate internal workflows, starting with automating Minutes of Meeting (MoM) generation, follow-up emails, and calendar coordination.
- Leverage CloudFront Edge Computing to optimize assets delivery costs, enforce automatic compression, and isolate origin servers using OAC.
- Recalibrate Production LLM Parameters: Transition critical systems to temperature = 0.1 and enforce strict structural validation via JSON mode to guarantee backend reliability.
- Pilot Multi-Agent source code deployments using Docker, Bedrock AgentCore, and Terraform to handle complex business logic requiring specialized validation layers.

### Event Experience

Attending this technology seminar series was a highly practical and invaluable experience. It provided a comprehensive upgrade to my technical perspective, ranging from cloud infrastructure resilience to cutting-edge Generative AI architectures. Notable highlights include:

#### Learning from highly skilled speakers
- Speakers from reputable tech organizations such as AWS, GoTymeX, Cloud Kinetics, and VPBank provided realistic, battle-tested engineering viewpoints.
- Gained deep insights into resolving actual enterprise pain points, from controlling volatile CDN bills to building automated financial underwriting engines for commercial banks.    

#### Hands-on technical exposure
- Observed live, end-to-end cloud environment demonstrations utilizing AWS S3, Amazon Bedrock, Amazon Q, and CloudFront.
- Witnessed practical case studies, including automated PM assistants and an interactive sketch-to-code tool powered by Claude Sonnet 4 built under a grueling 36-hour Hackathon timeframe.  

#### Leveraging modern tools
- Uncovered deep root causes of system behavior, such as GPU math limitations causing LLM variance, and structuring an enterprise-grade 3-layer Guardrail architecture.
- Learned how to dismantle monolith logical flows into specialized AI agents to resolve context dilution and single-point-of-failure challenges.  

#### Lessons learned
- In the age of AI, the precision and framework of your context always outshines the sheer mass of information provided (Context Quality > Context Quantity).
- Deploying AI for enterprise use-cases goes far beyond simply making a prototype run; it demands rigorous security, risk management, and strict regulatory compliance from day one.
- The most impactful, high-value technical innovations are almost always born from a hyper-focused effort to solve specific friction points encountered in daily operations.    

#### Some event photos
*Add your event photos here*  
![Event 1](/images/4-EventParticipated/event2.jpg)
> Overall, the event not only provided technical knowledge but also helped me reshape my thinking about application design, system modernization, and cross-team collaboration.
