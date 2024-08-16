ssue Summary
Duration: 2024-08-15, 10:00 AM to 11:30 AM GMT (1 hour 30 minutes)
Impact: RentHub, a platform connecting property owners with potential renters, experienced a significant outage affecting the search and booking functionalities. Approximately 85% of users were unable to access these critical features, leading to a large number of failed transactions and disrupted user experience.
Root Cause: The outage was traced back to a misconfigured database replication process that led to data inconsistencies and eventually caused the primary database to enter a read-only state.
Timeline
09:45 AM: Monitoring system detected an unusual spike in error rates across the platform.
09:50 AM: An alert was sent to the on-call engineering team, who started investigating the issue.
10:00 AM: The issue was confirmed as an outage with most users unable to search for properties or complete bookings.
10:10 AM: Initial investigation focused on the web server and load balancer configurations, assuming they were causing the slowdown.
10:30 AM: The database team was brought in after the web server analysis showed no abnormalities.
10:45 AM: Further investigation revealed inconsistencies in the database replication logs, leading to the discovery of the read-only state.
11:00 AM: The replication process was halted, and the database was manually reverted to a healthy state.
11:20 AM: The platform's services were gradually restored, with monitoring confirming normal operations.
11:30 AM: The outage was declared resolved, and the platform was fully operational.
Root Cause and Resolution
Root Cause: The root cause of the outage was a misconfiguration in the database replication settings. A recent update to the database cluster introduced a bug in the replication process, causing it to fail. When the replication failed, the primary database entered a read-only state to prevent further data corruption. This state disrupted the platform's ability to write new data, which directly affected the search and booking functionalities.

Resolution: The database team identified the issue by examining the replication logs and the database's read-only status. They halted the replication process and reverted the database to its previous stable configuration. A full backup was restored to ensure data consistency, and the replication settings were corrected. Once these changes were implemented, the system was thoroughly tested before bringing all services back online.

Corrective and Preventative Measures
Improvements/Fixes:

Replication Configuration Audit: Regular audits of database configurations will be scheduled to prevent misconfigurations.
Enhanced Monitoring: Additional monitoring will be implemented to detect database replication issues more quickly, including alerts specifically for replication failures and read-only states.
Incident Response Training: Conduct a review and training session with the engineering team to improve response time and accuracy in diagnosing future issues.
Tasks:

Patch Database Cluster: Apply a patch to the database software to fix the known replication bug.
Update Monitoring Tools: Configure monitoring tools to include checks for replication status and database write capabilities.
Review and Document Procedures: Document the incident and update the internal runbooks with detailed steps on how to handle similar database issues.
Automate Failover Process: Implement an automated failover process to switch to a backup database in case of primary database failure.
Conduct Post-Incident Review: Schedule a post-incident review meeting to discuss the lessons learned and refine the incident response process.
