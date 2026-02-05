# Observability Con - On The Road (February 5, 2026)

## Conference Overview

ObservabilityCON is Grafana's flagship conference, typically a 3-day event. The "On the Road" format condenses the highlights into a 1-day event held in various cities to reduce travel requirements for attendees. The Frankfurt edition took place on February 5, 2026, with approximately 200-250 attendees.

Conference website: https://grafana.com/events/observabilitycon-on-the-road/frankfurt

## Opening Keynote

The keynote served primarily as an introduction to Grafana as a company and a general call to action about utilizing available data. The speaker emphasized Grafana's deliberate commitment to open source, noting that the company intentionally maintains most features as open source and only uses a small portion for revenue generation. They highlighted that Grafana actively chooses not to monetize many potential revenue opportunities.

The concept of "adaptive telemetry" was introduced, following a cost hierarchy: Metrics > Logs > Traces > Profiles. Metrics are relatively inexpensive, logs less so, traces are large and expensive, and profiles are even more resource-intensive.

Various service models were discussed: Grafana Cloud, Grafana Open Source (on-premises), and a "bring your own cloud" option where Grafana operates a dedicated cluster for customers.

**AI Features Introduced**

The keynote teased AI capabilities for finding and analyzing issues. AI agents can check Prometheus, Loki, and other data sources for issues, all triggered through chat interactions. Users can simply click "Deep Investigation" and the agents scan all available data to provide reports that pinpoint the cause of an issue. This was demonstrated through a video presentation.

Key points about AI features:
- AI features are Grafana Cloud only
- AI investigations are currently in public preview
- Investigations can run before human intervention begins
- The person on call receives more comprehensive information immediately
- No plans to bring Assistant (AI) and Insights features to open source for on-premises deployments

**Technical Notes**

Grafana's AI does not use a specifically trained LLM. Instead, they invest heavily in prompt engineering. Grafana does not train models on customer data.

The speaker mentioned that organizations with high data privacy requirements use Grafana, including governments, space agencies, intelligence agencies, tech giants, and Formula 1 teams (implied to be using Grafana Cloud).

**Questions arising from keynote:**
- Is there room for improvement with Alloy in our setup? It offers a complete Prometheus pipeline - what exactly does this mean and what can it do? Or are we already doing the right thing by collecting logs, cleaning them up, and filtering them (only running pods) as data flows?
- What is eBPF through the instrumentation hub?

## Session: Full-stack observability: Faster root cause analysis with Grafana Cloud's knowledge graph

Grafana Cloud's "assets" are now the knowledge graph. The session focused on addressing complexity in modern systems where everything generates logs, metrics, and traces.

The solution bundle consists of: Knowledge graph, Insights, and RCA Workbench (Root Cause Analysis).

The Entities Catalog automatically discovers components and understands relationships between entities.

**Live Demo**

The demonstration showed a path from threshold breaches through all relevant components down to the database layer. The example showed that activating a feature flag caused issues, with the root cause traced to a SQL query. The system suggested replacing subqueries with joins. The AI can perform this analysis automatically and present findings.

This is a Grafana Cloud feature (at least implied). While presenters didn't explicitly say "not on-premises," cloud-only deployment was strongly implied.

## Session: From dashboards to decisions: How agentic AI is reshaping observability

Alerts can automatically trigger investigations and provide root cause data without human intervention.

The AI serves two primary purposes:
1. Troubleshooting
2. Information gathering (question answering)

The AI can generate dashboards based on descriptions, similar to other AI tools. However, it can also create dashboards based on investigation findings. This distinguishes it from external AI tools that lack Grafana's context and data.

## Session: Build a better reliability culture with AI + Grafana Cloud IRM, SLO, and Alerting

The session focused on reliability as paramount to building trust - positioning it as the most important feature. Maintaining reliability in changing environments (continuous feature implementation and deployment) is challenging.

**Key observation:** In the age of AI, more code is being written/generated, but potentially less code is fully understood due to AI-generated code. This means incidents will continue to happen - they always did, but it's now easier to provoke them. Reliability becomes more difficult to maintain.

Reliability is based on culture (people, processes, and tools).

The session emphasized incident handling processes and post-incident reviews (focusing on action items rather than just reporting) rather than technical dashboard implementation.

**IRM (Incident Response Management)**

IRM is integrated into the observability platform, eliminating context switching. For CPA, this would only work for systems using Grafana. Potential issues:
- We have multiple Grafana instances
- While this might help ops teams, it could introduce another information source for other stakeholders (one person's gain is another's loss)

**Question:** Is IRM a Grafana Cloud-only feature? The "Alerts and IRM" navigation point appears as "Alerts" only in our installation.

The technical portion demonstrated the IRM feature in Grafana and its interaction with alerts and investigations.

## Session: Smarter observability with Grafana Cloud: Collect the data you need, when you need it, and know what it costs

Focus: Adaptive telemetry (Cloud only).

**General principle:** Tracing is powerful and becomes particularly interesting when things don't work. In normal operation, trace data often goes unexamined. However, it's still necessary because without it, error cases aren't traced effectively. This creates a data storage challenge - tracing generates and stores large volumes of data.

**Adaptive Traces:** Keep only valuable traces. In Grafana Cloud, this reduces data volume and consequently reduces costs.

For on-premises Grafana Tempo, there's no automatic filtering or cleaning. If desired, this must be implemented manually. The challenge is determining what's "important." In Grafana Cloud, importance is determined through AI scanning all data for anomalies and patterns.

Adaptive traces continuously analyze trace data.

**Profiling**

Metrics, logs, and traces can feed into profiling, going from a signal to a specific line of code with code-level granularity. Consistently collecting profiling data enables identification of performance issues before they impact systems or users. This requires Grafana Pyroscope.

Profiling at code level can identify issues like "function X is called too frequently, causing performance issues." During investigation, Grafana can display CPU time per code line.

**Question:** How does Grafana know the code line? Does it need connection to a repository? Does it decompile? Another mechanism?

**Cost Management**

Cost management and billing should be treated as a first-class citizen. Monitor metrics like log line creation rates and alert on spikes. For example, an app might accidentally deploy with debug logging enabled in production.

The session focused on SaaS and Grafana Cloud context.

**Thoughts for CPA:** Cost management may be less critical since we run on our own infrastructure. However, it translates to capacity management. We don't want to over-pollute our MinIO bucket for Loki with debug messages. Better logging practices could enable longer retention periods at the same storage cost.

**Idea for discussion with teams:** How important are debug messages, particularly for certain environments? Options:
- Change log level settings for backends
- Use Alloy to scrape out debug messages and stop tracking them (might be better as it covers infrastructure apps as well)

**Note:** Traces work on-premises, but adaptive tracing is cloud only.

The AI determining which traces are important in Grafana Cloud also considers seasonal events like Black Friday or Christmas impacting online shops. However, customer-specific seasonal patterns must be learned by the AI over time.

## Session: From closed vaults to open standards: How Erste Digital unlocked observability with OpenTelemetry and Grafana Cloud

Context: Banking environment (regulated industry).

**Presenter note:** This was the weakest session, possibly because the speaker appeared less comfortable presenting in English to a large audience.

**Key points:**
- As a bank, they operate very old infrastructure including mainframes and legacy systems
- They addressed regulatory requirements through an in-house gateway that all data passes through before reaching Grafana Cloud
- The gateway harmonizes data from diverse sources (no specific details provided on functionality)
- They reduced onboarding time from weeks to days for teams wanting to observe their applications

**Lesson learned:** Treat labels carefully. Excessive labels can create cardinality hell. Many labels with individual data points create numerous indexes/series in Loki, impacting performance. Recommendation: be careful with label quantity and design.

## Session: Deploying OpenTelemetry with Grafana Cloud

**Observability Hierarchy:**

1. **Infrastructure visibility** (lowest level): Alloy, Node Exporter, and other exporters provide this
2. **Baseline service visibility**: Black-box application observation - availability and health
3. **Deep transactional insights**: Connecting network requests with applications, correlating logs, metrics, traces, and all signals. OpenTelemetry excels here. Frameworks exist for Java to publish OTel data
4. **Custom application logic** (top layer): Custom data and business logic integration

The remainder of the session demonstrated "one-click" integration in Grafana Cloud through the Implementation Hub.

**Not applicable to CPA:** We don't use Grafana Cloud. Our "one-click solution" requires more manual work - writing Kubernetes manifests and deciding what to monitor from where. However, it rolls out to all clusters through ArgoCD. The Prometheus Operator provides significant automation for service discovery in our clusters, eliminating the need to manually point to endpoints.

## Session: Reliability from the outside in: How Grafana Cloud helps you see what your users experience

Alloy and exporters provide data from inside the cluster. Outside-in monitoring mimics what users see and how they access the system.

The external environment is chaotic and contains factors beyond our control: connection speeds, browser choices, etc.

**Grafana's approach:**
- Grafana Cloud Synthetic Monitoring
- Grafana Cloud Frontend Observability
- Grafana Cloud k6

**k6 Studio** allows recording interactions with a website and generating JavaScript test cases. CPA has already used k6 for Kafka load tests. In Grafana Cloud, tests can be run from different global locations (essentially AWS regions). Custom probes are also possible - for example, checking if services are available and performant from Indonesia.

k6 use cases:
- Load tests (as we've already done)
- Regression tests by recording and automating user cases
- Could assist with load testing

The Grafana Cloud features appear valuable. However, running probes across the globe seems to be the unique cloud component. Running tests and recording user interactions can be done from our infrastructure as well.

Grafana Cloud can track HTTP requests with detailed breakdowns and provides screenshots of the web application at different stages, showing how the app appears to users.

## Conversation with Grafana Team Member

At one of the conference stands, I spoke with a Grafana employee about our approach using ArgoCD for automatic deployments and operators managing dashboards through Custom Resources (CRs). He responded positively and appreciated the approach.

## Current State Assessment

We're already implementing several observability practices effectively. However, in many areas we're only scratching the surface. Observability in the cloud offers significantly more capabilities, including:
- Auto-discovery of clusters and microservices
- Automatic data collection from JVM or Linux kernel with Alloy (and additional tooling support)

## Post-Conference Reflection

**Was the initial assessment still valid?**

Yes. The initial assessment from the keynote held true after attending all sessions. While the keynote teased AI capabilities, the sessions provided the impressive technical details and concrete demonstrations. The feature set available in Grafana Cloud is substantially more comprehensive than on-premises offerings. Although the speaker mentioned most features are available as open source, the AI capabilities dramatically accelerate information collection, issue investigation, and summarization, creating a significant practical feature gap between cloud and on-premises deployments.

**Personal opinion:**

The trip to Frankfurt was worth it. The AI features demonstrated throughout the sessions look genuinely helpful and interesting. I'm curious about these capabilities and would like to explore them further. However, the reality is that many of these features cannot be tested at CPA because AI features are Grafana Cloud only. This limitation is disappointing given the potential value these tools could provide for faster incident resolution and more efficient observability workflows.

## Ideas to Explore

Based on conference insights, the following areas warrant investigation:

### 1. Auto-Discovery Capabilities
- Explore auto-discovery features for clusters and microservices in current on-premises setup
- Investigate available auto-discovery features without cloud/AI dependencies

### 2. Alloy for Data Collection
- Test Alloy for automatic data collection from JVM
- Evaluate Alloy for Linux kernel metrics collection
- Assess additional tooling requirements and integration possibilities

### 3. Operator and CR Enhancements
- Expand the ArgoCD + operator pattern (since it was well-received)
- Explore additional dashboard and configuration management through CRs

### 4. Open Source Feature Parity
- Investigate which features mentioned as "open source" in sessions are actually available for on-premises deployment
- Evaluate the gap between cloud AI features and achievable results with open source alternatives

### 5. Observability Depth
- Identify specific areas where we're "scratching the surface"
- Prioritize deeper implementation of existing observability capabilities before pursuing new features

### 6. Log Level Management
- Discuss with teams: how important are debug messages for various environments?
- Consider adjusting log level settings for backends or using Alloy to filter debug messages

## References

- Grafana Adventure GitHub repository: https://github.com/grafana/adventure
- Look into public dashboards from Wikimedia

## Open Questions

- Is there an official Helm Chart for Grafana Tempo Operator?
- How does Grafana profiling identify specific code lines? (Repository connection? Decompilation? Other mechanism?)

---

*Conference: ObservabilityCON On the Road*  
*Location: Frankfurt, Germany*  
*Date: February 5, 2026*  
*Attendees: ~200-250 people*
