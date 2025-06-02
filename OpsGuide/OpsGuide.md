**Ops Guide: Operational Best Practices**
This guide summarizes best practices and principles to help teams effectively manage their workloads and applications operationally.

**Introduction: The Culture of Operational Excellence**
Operational Excellence (OE) is our commitment to building software correctly while consistently delivering a great customer experience. It is a culture focused on delivering software that is scalable, reliable, resilient, frugal, efficient, and performant, which in turn allows teams to spend more time building new features and less time on maintenance and fighting fires. Operational Excellence is fundamental to Customer Obsession. Deferring OE can lead to issues that become overwhelming. We bake OE into every part of the development lifecycle to achieve continuous improvement.

**Key Principles of Operational Excellence**
Maintaining operational excellence at scale requires vigilance and rigor across three critical areas: scalability, performance, and availability. Other key aspects and considerations include:
*   **Scalability:** How well a service handles increased loads. Systems must easily grow to meet customer needs. Design principles include eliminating single points of failure, scaling horizontally, prioritizing asynchronous workflows, using caching effectively, and designing for maintainability and automation.
*   **Performance:** Ensuring systems operate efficiently.
*   **Availability:** How often a service is up and running. We do not take planned downtime and works hard to avoid unplanned downtime. Our Region and Availability Zone model is a recommended approach for high availability applications.
*   **Resilience:** The ability of systems to recover quickly from failures or withstand disruptions. Designing systems to withstand single host failure, AZ loss, and dependency failures is crucial.
*   **Security:** Security is fundamental to success. It is a shared responsibility; We manage the security *of* the cloud, while customers are responsible for security *in* the cloud. Employing best practices and services helps defend against bad actors. Physical data center security, network separation, hardware isolation, and storage isolation are employed.
*   **Sustainability:** Building and running infrastructure in an environmentally friendly way is a commitment. Optimizing resource usage and leveraging energy-efficient technologies contribute to sustainability goals. Sustainability is becoming a key factor in cloud purchase decisions.

**Operational Practices**

1.  **Monitoring and Alarming**
    *   Use monitoring and alerting capabilities to get early warning when key operational metrics thresholds are crossed.
    *   Define key metrics and monitoring scope, identifying critical KPIs and the scope across service components and backend applications.
    *   Leverage (insert your favorite monitoring solution) to gather and analyze metrics and logs. Operational dashboards using tools like CloudWatch and iGraph display key metrics and service health in real-time.
    *   Dashboards should include load balancer metrics and metrics for critical dependencies. Regularly review operational dashboards, often daily, to monitor system health and identify areas for improvement.
    *   Set tightly set thresholds for alarms to alert the right resolver. High-severity alarms should trigger and alert engineers when the service behaves unexpectedly.
    *   Ensure each log message includes sufficient relevant information for understanding system behavior. Logs provide granular insights to diagnose incident root causes.
    *   Use canaries to continually test service functionality by simulating customer traffic outside the service layers. Onboard canaries for public services.
    *   Configure alarms to alert to blocked pipelines via SIM.
    *   Monitor security events and track security-related metrics to identify potential threats.

2.  **Incident Response and Root Cause Analysis**
    *   The first priority while oncall is to **mitigate high severity events** and restore systems quickly.
    *   Escalate Early! It is better to escalate too soon than too late. TechOps coordinates responses to large scale events (LSEs).
    *   Operational related events are resolved according to service team runbooks.
    *   Use the Correction of Errors (COE) process, our structured mechanism for learning from operational incidents. COEs involve writing a document that exposes the root cause(s), itemizes learnings, and lists actions to prevent reoccurrence. The purpose is to improve systems, not assign blame.
    *   Identify root causes quickly after an event when logs and metrics are still relevant. Don't add root-causing to a backlog.
    *   High-severity alarms should auto-create tickets that include links to relevant monitors, dashboards, and runbooks to streamline response.

3.  **Oncall Management**
    *   Oncall is a primary way to demonstrate Ownership and Customer Obsession. It requires being available quickly to resolve customer pain.
    *   Prepare for oncall rotations by shadowing a teammate, learning your team's procedures, reviewing runbooks, and knowing how to escalate. Complete required trainings like Tier 1 Resolver Training and Operational Excellence training.
    *   While oncall, priorities include mitigating high severity events, protecting team productivity, and escalating early.
    *   Address all High Severity alarms/tickets, follow up on tickets, and check pipelines.
    *   Use ticket etiquette to document work (metrics reviewed, commands executed, logs analyzed) in the worklog and share findings in the communication tab. A ticket is an artifact of work and plays a role in career growth.
    *   Take time to relax and rest after long durations oncall.
    *   Conduct a post-mortem review after go-live to discuss what went well, what didn't, and opportunities for improvement.

4.  **Deployment and Change Management**
    *   Deploy most changes through automated code pipelines.
    *   For out-of-band changes to production systems, use Change Management (CM) tickets. CMs require approval from a CM Bar Raiser. Many tools require the **2-person rule** for safe execution. Using the Change management tool for non-critical operations is an anti-pattern.
    *   Operational tools used for changes to production must be treated as production software. Changes to the tool code should be reviewed and deployed through a pipeline. Access limitations must be enforced.
    *   Implement automated Continuous Integration/Continuous Deployment (CI/CD) pipelines for efficient, reliable updates.
    *   Changes to services should be reviewed and tested in a series of pre-production environment stages (e.g., alpha, beta, gamma, pre-prod, one-box, prod). Promotion to the next stage is blocked if testing failures are identified.
    *   Production releases should be **sequentially deployed** to a minimal footprint environment based on system topology, where they are tested and monitored before full deployment (canary deployments). Gradually propagate to additional hosts and deployment "waves".
    *   Implement automated rollback mechanisms in pipelines when deployments fail or monitoring thresholds are breached. **Roll back liberally** if a problem occurs after deployment; don't ponder or diagnose first. Ensure rollback steps are defined and enforced for manual changes (e.g., using MCM tickets).

5.  **Testing**
    *   Perform load testing on an as needed basis to understand performance constraints and capacity limits/thresholds. Conduct large-scale load tests against your production environment before launch and quarterly.
    *   Implement automated testing (unit, integration) as part of CI/CD pipelines.
    *   Conduct gameday exercises to test operational behavior/recovery of systems and team response processes. Gamedays test failure modes, verify recovery, and validate alarms, runbooks, and oncall response. Include load testing in gamedays.
    *   Verify reporting accuracy and functionality through testing.

6.  **Capacity Planning**
    *   Service teams perform capacity management reviews at least monthly, reviewing demand, infrastructure needed, risks, and mitigation plans.
    *   Use data-driven forecasting models based on current/historical usage and customer input.
    *   Capacity plans should account for brief load spikes (e.g., 2x expected TPS) and single AZ failures.
    *   Request additional incremental capacity through internal systems.

7.  **Operational Reviews and Reporting**
    *   Complete Operational Readiness Reviews (ORRs) before launching a service and annually post-launch to ensure readiness and track identified risks. ORRs assess monitoring, alarming, documentation, and testing. ORRs are completed in the CloudReadiness tool.
    *   Conduct weekly operations review meetings to improve service availability and mitigate operational risks. Review operational dashboards, COE items, Policy Engine risks, and patching status in these meetings.
    *   Conduct monthly and quarterly business reviews and project/program status reporting to keep management informed about operational issues, risks, and key business metrics. These provide transparency, oversight, and escalation paths.
    *   Establish operational and performance objectives for risk reduction during the annual planning process (OP process). These goals are tracked in an internal application like Kingpin.

8.  **Security Best Practices**
    *   Apply the **principle of least privilege**, ensuring users and systems only have necessary access.
    *   Encrypt all data in transit and at rest and in processing if possible.
    *   Validate all inputs to prevent injection attacks. Ensure all output is encoded and sanitized.
    *   Add security test cases to pipelines to verify unauthorized access is prevented.
    *   Conduct application security reviews, including architecture reviews and threat modeling, driven by the development team.
    *   Use Tag-Based Access Control (TBAC) for security in environments with multiple business units.
    *   Leverage services for intelligent threat detection.
    *   Adhere to security and regulatory requirements, ensuring compliance.

9.  **Resilience and Disaster Recovery**
    *   Design services to operate independently in each AZ to prevent a disruption in one AZ from causing an event in others (AZ Independence).
    *   Design services to withstand the loss of an availability zone without interruption to core functions. Proof includes data replication across AZs, DB cluster failover, agent retry mechanisms, and load balancers with health checks. Maintain runbooks for shifting away from an impaired AZ.
    *   Design services to withstand dependency failures through mitigations like timeouts, circuit breakers, retries, spare capacity, credential caching, limits, throttling, and fail fast.
    *   Develop a comprehensive Disaster Recovery (DR) strategy for business continuity. Define Recovery Time Objective (RTO) and Recovery Point Objective (RPO). Identify critical data, applications, integration points, and the total cost of an outage. Develop detailed procedures for handling disruptions.

10. **Sustainability Considerations**
    *   Utilize internal tools to measure estimated carbon emissions from cloud usage.
    *   Understand workload impact, measure progress, and model targets.
    *   Optimize resource usage and select energy-efficient compute options like custom silicon, arm64 or other power efficient compute.
    *   Work with our internal sustainability experts to improve solution sustainability.

**Continuous Improvement**
When falling short of operational goals, quickly identify root causes, learn from mistakes, and invest in solutions to prevent future issues. The COE process is a key mechanism for learning and driving improvements. Oncall is also a time to drive engineer-facing improvements. Develop and implement a continuous improvement plan based on insights gained during the post-go-live period.

