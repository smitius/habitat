I tried to compile coding and operational best practices for developers creating, maintaining, or adding features to a new service, drawing on principles of operational excellence, availability, security, and specific coding guidelines:

**Operational Excellence as a Foundation**
Operational excellence is a commitment to building software correctly while consistently delivering a great customer experience. It is a culture of delivering scalable, reliable, resilient, frugal, efficient, and performant software that delights customers. Getting operational excellence right allows teams to focus more time on building new features and less on maintenance and fighting fires.

**Key Aspects of the Software Development Lifecycle**

1.  **Design:**
    *   Software/system designs must go through a design review before development starts. Designs should be signed off, ideally by a Principal engineer.
    *   Consider the "7 C's" when evaluating designs: Customer (is it what they want, typical/outlier use cases), Complexity (is it as simple as possible, minimal moving parts), Compartmentalization (blast radius protection, fault isolation), Correctness (obvious bugs, corner cases), Completeness (addresses all requirements), Consistency (internal and external), and Communication (people needed, collaboration process).
    *   Follow scalability design principles like eliminating single points of failure, scaling horizontally, prioritizing asynchronous workflows, using caching effectively, and designing for maintainability and automation.
    *   Ensure robust failure handling mechanisms are designed, such as timeouts, circuit breakers, retry logic, spare capacity buffers, credential caching, limits and throttling, and failing fast to limit queues.
    *   Architecture design should consider durability best practices, determining what data is recoverable, defining Recovery Time Objectives (RTO) and Recovery Point Objectives (RPO) for restoration, specifying backup frequency, and setting up alarms for backup failures.
    *   Services should be designed with defined throttling techniques to protect themselves from customers, considering default throttle limits relative to dependencies and integrating with Service Quotas. Default throttle and resource limits should be defined, noting which are hard and soft.

2.  **Coding:**
    *   Follow general coding principles: code should be logical, maintainable, and tested.
    *   Establish and follow team coding guidelines, which tailor coding standards to the team's needs and are used in the code review process. Consistency of style and adherence to standards across a system reduces long-term maintenance costs.
    *   Code should be well-documented. Document the 'Why' (motivation, problem solved), 'What' (function purpose, side effects, higher-level view), and 'How' (design level) of your code. Assume language fluency, but do not assume prior knowledge about your program. Fix missing or incomplete documentation. Avoid documenting the obvious or simply translating code into English; use good variable names instead.
    *   For Java, follow common coding recommendations, prioritizing readability. Consistency in indentation is crucial. Always use brackets for single statement if/else/for/while. Alignment that enhances readability is encouraged. For C++, packages must live in Brazil and use the standard build system.
    *   Ensure identifiers (customer visible or internal) are larger than reasonably required.
    *   Intentionally set appropriate retry and socket timeout configuration for all SDK usage.

3.  **Code Review:**
    *   Code reviews are a critical company best practice and are important for learning and teaching.
    *   All code and configuration destined for production, including internal tools, should be reviewed by another developer before being pushed, if possible. The author and reviewer must reach consensus. Reviewers share accountability for code quality.
    *   Code reviews should be supportive and collaborative, focusing feedback on the code itself, not the author. Do not block reviews on matters of personal preference or style.
    *   Ensure every change has associated unit and integration tests. Do not change/add production code without changing/adding tests. Code reviews without tests should not be approved ("Ship It").
    *   Look for: Clarity, Correctness (including thread safety and unit tests), Design Implications, Reuse and Duplicated Code, Configuration and Constants, Backwards Compatibility and Versioning, Dependencies, Failure Handling, Performance, Code Style, and Security issues.
    *   Critically, code reviews are essential for identifying and mitigating security risks. Check for hardcoded credentials, sufficient logging (who, when, what actions), logging of authentication failures, and generic error messages. Add security test cases to your pipelines. All code must be reviewed for security issues, with requirements dependent on the application risk classification. Automated security review tools should be used. Findings from Crux Analyzer tools MUST be addressed and shall NOT be overridden.
    *   Require a minimum of two approvers for every merge. Avoid overriding and merging unless dealing with a critical emergency.

4.  **Testing:**
    *   Implement automated Continuous Integration/Continuous Deployment (CI/CD) pipelines and Test-Driven Development (TDD) practices. Modern DevOps, which includes automated CI/CD and TDD, significantly improves business outcomes, including operational resilience.
    *   Automated tests should be created for components like Lambda functions, contact flows, and integrations, ensuring comprehensive test coverage with realistic data.
    *   Unit tests should be written for modules/packages, checked into source control, and run as regression tests prior to releases. Unit tests should run as part of the build process, be sandboxed, and fail the build when they fail. Commit to maintaining unit test code coverage levels above a defined bar (e.g., at least 70% general purpose), potentially blocking check-ins or deployments if below.
    *   Integration tests should maintain coverage for 100% of public APIs and critical user scenarios. Integration tests should run automatically as approval steps between stages in the pipeline. Pre-production testing in various stages (Alpha, Beta, Gamma) is required, and promotion to the next stage is blocked if testing failures are identified.
    *   Load testing should be performed as needed to understand performance constraints and capacity limits. Load testing is performed in pre-production environments to verify the system's response to traffic and determine latency and throughput. Load testing should be performed for new features before deploying to production, and code/configuration changes should be regularly load tested for performance regressions.
    *   Canaries (external probes simulating customer requests) should be used to test system functionality and reliability, particularly for availability, latency, and security. Canaries must test all control plane and data plane APIs, critical customer scenarios, and UIs in all regions.
    *   Game day exercises should be performed to test the operational behavior/recovery of systems and team response processes.

5.  **Deployment:**
    *   Use pipelines to deploy all software, configuration, and infrastructure. Minimum expectations for pipelines are documented.
    *   Deployments should be frequent and gradual to minimize risk. Production releases should be sequentially deployed to a minimal footprint environment (e.g., one AZ in one region), where they are tested and monitored before full deployment. Each production deployment should have a bake time for continuous testing and monitoring. Customer-impacting deployments should first deploy to non-production stages, and failures in non-prod should block deployment to production.
    *   If something goes wrong, roll back first and investigate later. Use auto-rollback monitors in pipelines, connected to important business metrics like availability and latency. Ensure rollback steps are configured in deployment tools or modeled change management (MCM) tickets.
    *   Manage load balancer host deregistration and reregistration activities during deployments to instances/hosts. Ensure that at least 66% of capacity in each production stage remains healthy during deployment.
    *   Infrastructure managed via CloudFormation should follow the same scrutiny as software changes, including code reviews, change control, and deployment via pipelines. Use CloudFormation Change Sets to validate the intent of stack updates. Test Stack Updates in Gamma before promoting to Production. Apply Stack Policies to protect critical resources. Partition resources across stacks to reduce blast radius. Use Drift Detection to detect changes made outside of CloudFormation.

6.  **Operations & Maintenance:**
    *   Own your operations roadmap. Proactively look for impending risks like scaling limits, rather than just reacting to problems.
    *   Establish and maintain monitoring and alerting capabilities to provide early warning when key operational metrics thresholds are crossed. Use standard techniques like instrumentation, operational dashboards, canaries, and alarms. Monitor customer/client metrics (latency, availability, error rates), service utilization metrics (resource usage, capacity planning), and diagnostic metrics. Publish customer resource usage metrics to CloudWatch. Production systems must have appropriate monitoring alarms that catch all known potential production issues.
    *   Maintain runbooks to aid and inform engineers in handling incidents or issues. Operational events should be resolved according to service team runbooks.
    *   Define a process and mechanisms to notify customers of operational issues affecting their service, using standard processes like "Habitat" Health Service or similar.
    *   Conduct weekly operations review meetings to improve service availability and mitigate operational risks.
    *   Call for help when you are stuck during a customer-impacting event. Escalate early.
    *   Address security incidents promptly. Cloud Native approaches contribute to a reduction in security incidents. Modern DevOps reduces the time required to resolve downtime incidents. Managed Databases reduce production failures for new features/services. Containers reduce time to detect security incidents and production failures. Open Source adoption reduces time to resolve downtime incidents. Highly modernized organizations experience significant reductions in production failure rates and time to resolve downtime incidents.
    *   Regularly perform capacity management reviews (at least monthly) to review demand, needed infrastructure, risks, and mitigation plans.
    *   Operational tools must be treated as production software. Changes to operational tools should be code reviewed and deployed through a pipeline. Tools commonly used to make changes to production may require the 2-person rule or allowance listing for single person operations.

7.  **The Ten Commandments of Habitat Availability:** Adhere to these inviolable rules to ensure high availability:
    *   Do not damage multiple Regions or locations at the same time by deploying all at once.
    *   Deploy changes frequently and gradually.
    *   Roll back liberally if a problem occurs after deployment.
    *   Do not use Black Boxes (technology where we are reliant on a 3rd party for debugging/patching or don't exactly know what its doing).
    *   Do not blame dependencies; own your service availability including dependencies and drive their resolution.
    *   Do not touch production without a Change Management (CM) ticket for out-of-band changes.
    *   Own your operations roadmap.
    *   Call for help when stuck during an operational event.
    *   Be transparent to build trust, share learnings, and get help. (The 10th commandment isn't explicitly listed as a heading, but transparency is mentioned last in the list of rules).
