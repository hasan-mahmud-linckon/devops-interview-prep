# DevOps & Cloud Engineer – Interview Question Bank  
**Candidate: Hasan Mahmud**  
*Based on Resume & Experience at Penciltech, Shell Technologies, Wafi Solutions*

---

## 1. Tell me about yourself and your DevOps journey.

**Answer:**  
I'm Hasan Mahmud, a DevOps & Cloud Engineer with over a decade of experience in software development and infrastructure automation. I started as a Software Engineer, working extensively with C#, ASP.NET, and Angular, which gave me a strong full-stack foundation. Over time, I transitioned into DevOps, focusing on cloud platforms, CI/CD pipelines, containerization, and infrastructure as code.

In my current role at **Penciltech**, I’ve led the migration of a SaaS platform from VPS to AWS, implemented Docker and Ansible for consistent deployments, automated SSL renewals, and set up observability with Grafana and Loki. I’ve also built robust CI/CD pipelines using GitHub Actions and Jenkins. My blend of development and operations experience allows me to bridge gaps between teams and deliver scalable, reliable systems.

---

## 2. You mentioned migrating a SaaS platform from VPS to AWS. Can you walk me through that process?

**Answer:**  
Yes. At Penciltech, we were running a SaaS application on traditional VPS environments, which lacked scalability and high availability. To modernize the infrastructure, I led the migration to **AWS**, using:

- **EC2** for compute instances with auto-scaling groups for elasticity.
- **RDS (MySQL)** for managed, highly available databases with automated backups and snapshots.
- **S3** for secure, durable storage of user uploads and static assets.

I used **Terraform** to define the infrastructure as code, ensuring reproducibility across environments. I also **Dockerized** the application services to ensure consistency between development and production. The migration improved system scalability, reduced downtime, and enabled faster deployment cycles.

---

## 3. How did you ensure consistency in deployments? What tools did you use?

**Answer:**  
To ensure consistent deployments, I leveraged **Docker** and **Ansible** together:

- I **containerized** the application services using Docker, which encapsulated dependencies and environment configurations.
- I wrote **Ansible playbooks** to automate server provisioning, Nginx configuration, and Docker service deployment.
- This combination allowed us to achieve **repeatable, idempotent deployments** across staging and production environments, reducing configuration drift and human error.

Additionally, all deployment workflows were triggered via **CI/CD pipelines** in GitHub Actions, further minimizing manual intervention.

---

## 4. How did you automate SSL certificate renewals in Docker?

**Answer:**  
We were using **Nginx as a reverse proxy** in Docker containers with Let’s Encrypt SSL certificates. The challenge was preventing certificate expiry during container restarts or redeployments.

To solve this:
- I wrote a **Bash script** that checks the certificate expiry date using `openssl`.
- If the certificate is within 30 days of expiry, it triggers `certbot` to renew it.
- This script is scheduled via **cron inside the container**, running daily.
- The renewed certificates are automatically reloaded in Nginx using `nginx -s reload`.

This automation eliminated manual renewal tasks and prevented any service disruption due to expired certificates.

---

## 5. Describe your CI/CD pipeline setup using GitHub Actions.

**Answer:**  
At Penciltech, I designed and maintained **GitHub Actions pipelines** to automate testing, building, and deployment.

The pipeline includes:
- **Trigger:** On push to `develop` (deploy to staging) and `main` (deploy to production).
- **Jobs:**
  - Run unit and integration tests.
  - Build Docker images with proper tagging (e.g., commit SHA).
  - Push images to a private ECR registry.
  - SSH into the target server (or use Ansible) to pull the new image and restart services.
- I also established **Git branching strategies** (e.g., feature branches, PR reviews) to reduce release errors and improve code quality.

This setup reduced deployment time from hours to minutes and improved release reliability.

---

## 6. You used Grafana Loki. Why did you choose it, and how did it help?

**Answer:**  
We needed a lightweight, scalable solution for **centralized log aggregation** to troubleshoot application and Nginx issues faster.

I chose **Grafana Loki** because:
- It’s cost-effective (indexes only metadata, not full logs).
- Integrates seamlessly with **Prometheus and Grafana**.
- Works well with Docker and structured logging.

I configured Docker’s logging driver to send logs to Loki using **Promtail**. Once set up, teams could:
- Search logs across services in real time.
- Correlate logs with metrics in Grafana dashboards.
- Identify errors quickly (e.g., 5xx responses in Nginx).

This reduced mean time to resolution (MTTR) significantly.

---

## 7. How do you manage infrastructure as code? Which tools do you use?

**Answer:**  
I use **Terraform** as the primary IaC tool for provisioning cloud resources on AWS. For example:
- Defined VPCs, subnets, security groups, EC2 instances, RDS, and S3 buckets in `.tf` files.
- Used **remote state storage in S3 with DynamoDB locking** to enable team collaboration and prevent conflicts.
- Applied `terraform plan` and `apply` in CI/CD pipelines with proper approvals.

For configuration management, I use **Ansible** to:
- Install and configure software (e.g., Docker, Nginx).
- Deploy applications and manage secrets.

This combination ensures infrastructure is **version-controlled, auditable, and reproducible**.

---

## 8. What monitoring and observability tools have you worked with?

**Answer:**  
I’ve worked with a full observability stack:
- **Prometheus**: For scraping and storing metrics from Docker, Node Exporter, and applications.
- **Grafana**: To visualize metrics (CPU, memory, request rates) and create dashboards for uptime and performance.
- **Loki**: For log aggregation from Docker and Nginx.
- **ELK Stack (Elasticsearch, Logstash, Kibana)**: Previously used at other roles for structured log analysis.

I also set up **alerting rules in Prometheus** (e.g., high error rates, disk pressure) and routed them to Slack or email via Alertmanager.

---

## 9. You have strong full-stack experience. How does that help in your DevOps role?

**Answer:**  
My background as a **Senior Software Engineer** in ASP.NET, Angular, and cloud services gives me a unique advantage:

- I can **collaborate effectively with developers**—I understand their pain points, logging practices, and application architecture.
- I can **optimize CI/CD pipelines** based on the app’s tech stack (e.g., .NET build steps, Angular bundling).
- I can **troubleshoot issues faster** because I understand both code and infrastructure layers.
- I’ve even contributed to application code (e.g., adding health checks, structured logging) to make systems more observable and cloud-native.

This full-stack insight helps me design DevOps solutions that are practical, efficient, and developer-friendly.

---

## 10. Have you worked with Kubernetes? If so, describe your experience.

**Answer:**  
Yes, I have hands-on experience with **Kubernetes** in test and staging environments.

I’ve:
- Deployed containerized applications on **EKS** and **Minikube**.
- Written manifests for Deployments, Services, Ingress, and ConfigMaps.
- Used **Helm** for templating and managing application releases.
- Integrated Kubernetes with **Argo CD** for GitOps-style continuous delivery.

While my current role uses Docker Compose for now, I’ve advocated for Kubernetes adoption to improve scalability and resilience, especially as the SaaS platform grows.

---

## 11. What is GitOps, and have you used Argo CD?

**Answer:**  
**GitOps** is a methodology where the desired state of infrastructure and applications is stored in Git, and automated tools ensure the system matches that state.

I’ve used **Argo CD** as a GitOps tool to:
- Sync Kubernetes applications from a Git repository automatically.
- Provide a dashboard for deployment status and rollback capabilities.
- Enable declarative, auditable, and automated deployments.

At Penciltech, I’ve started exploring Argo CD for future container orchestration, aiming to reduce manual deployments and improve rollback safety.

---

## 12. How do you handle database migrations in CI/CD?

**Answer:**  
Although not explicitly in my current role, in past full-stack projects (e.g., Pension Portal, Recruitment System), I handled database migrations using:

- **Entity Framework Core Migrations** in .NET apps.
- Scripts were version-controlled and applied via CI/CD after deployment.
- For production, I used a **manual approval step** in the pipeline to execute migrations safely.
- Backups were taken before applying changes.

In DevOps contexts, I’d integrate tools like **Liquibase** or **Flyway** for database versioning, especially in microservices environments.

---

## 13. How do you ensure security in your DevOps practices?

**Answer:**  
Security is integrated into every layer:
- **Secrets Management**: Used AWS SSM Parameter Store and environment variables (not hardcoded).
- **IAM Roles & Policies**: Applied least privilege access for EC2 and services.
- **Secure CI/CD**: Protected main branches, required PR reviews, scanned code for vulnerabilities.
- **Container Security**: Scanned Docker images using tools like Trivy in pipelines.
- **Network Security**: Configured security groups, private subnets, and WAF where needed.
- **Compliance**: Followed best practices for data encryption (at rest and in transit).

In previous roles, I also worked on **cybersecurity dashboards**, giving me deeper insight into security monitoring.

---

## 14. Describe a challenge you faced in DevOps and how you solved it.

**Answer:**  
One challenge was **frequent deployment failures due to environment inconsistency**.

Developers tested locally, but apps failed in staging due to config differences.

**Solution:**
- I **Dockerized** all services, ensuring the same environment everywhere.
- Used **Ansible** to automate configuration.
- Introduced **GitHub Actions** with automated testing and staging deployments.

Result: Deployment success rate improved from ~70% to 99%, and troubleshooting time dropped significantly.

---

## 15. Where do you see yourself in 3–5 years?

**Answer:**  
I aim to grow into a **Senior DevOps or Cloud Architect** role, leading cloud transformation initiatives and mentoring junior engineers. I want to deepen my expertise in **Kubernetes, serverless, and FinOps**, and contribute to building resilient, cost-efficient, and automated cloud platforms. I’m also passionate about **GitOps and platform engineering**, and I’d like to help build internal developer platforms that empower teams to ship faster and safer.

---

## Bonus: Quick-Fire Technical Questions

| Question | Answer |
|--------|--------|
| **What is the difference between Docker and Kubernetes?** | Docker containers apps; Kubernetes orchestrates and manages containers at scale. |
| **What is a blue-green deployment?** | Two identical environments; traffic switches from blue (old) to green (new) after testing. |
| **Explain CI vs CD.** | CI = automated builds/tests on code change; CD = automated deployment to production. |
| **What is a VPC?** | Virtual Private Cloud – isolated network in AWS for secure resource hosting. |
| **How does Terraform state work?** | Tracks real-world resources; stored remotely (e.g., S3) for team sync. |
| **What is a sidecar container?** | A helper container in the same pod (e.g., for logging or monitoring). |

---

## 💡 Tips for the Interview
- **Use the STAR method**: Situation, Task, Action, Result.
- **Quantify results**: “Reduced deployment time by 80%”, “Improved uptime to 99.9%”.
- **Be ready to whiteboard**: Draw your AWS architecture or CI/CD flow.
- **Ask smart questions**: “Do you use GitOps?”, “How do you manage cloud costs?”

---

### ✅ Prepared for:  
DevOps Engineer, Cloud Engineer, Site Reliability Engineer (SRE), Platform Engineer

📅 **Last Updated:** May 2025  
👤 **Candidate:** Hasan Mahmud  
📍 Dhaka, Bangladesh  
📧 [Your Email] | 🔗 [LinkedIn] | 💼 [GitHub]
