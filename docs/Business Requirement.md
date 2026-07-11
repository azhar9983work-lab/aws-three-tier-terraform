Business Requirement

AcmeShop is an e-commerce startup. Initially, they deployed everything on a single EC2 instance:

Internet
     │
EC2 Instance
     │
MySQL

This worked when there were only a few hundred users.

Now they have problems:

During sales, the server crashes.
Deployments cause downtime.
If the EC2 instance fails, the entire application is unavailable.
The database is publicly accessible, creating a security risk.
Manual server setup leads to configuration drift.
There is no monitoring or alerting.