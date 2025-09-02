DevOps CI/CD Workflow
This flowchart outlines a typical end-to-end DevOps workflow, from initial planning to production deployment and ongoing operations.

``` mermaid
graph TD
    subgraph "1. Plan & Code"
        A["💡 Idea / Business Requirement"] --> B["📝 Create Task in Project Management Tool <br> (e.g., Jira)"];
        B --> C["🌿 Developer Creates New Git Branch"];
        C --> D["💻 Developer Writes Code & Unit Tests"];
        D --> E["🚀 Push Code to Git Repository"];
    end

    subgraph "2. Continuous Integration (CI)"
        E --> F{"CI/CD Pipeline Triggered <br> (e.g., Jenkins, GitHub Actions)"};
        F --> G["📥 Fetch Latest Code"];
        G --> H["🔍 Static Code Analysis & Linting"];
        H --> I["🛠 Build Application"];
        I --> J["🧪 Run Automated Unit & Integration Tests"];
        J -- "Fails" --> K["❌ Notify Developer & Stop"];
        J -- "Passes" --> L["📦 Package Application into a Docker Image"];
        L --> M["📤 Push Docker Image to Container Registry"];
    end

    subgraph "3. Infrastructure & Configuration (IaC)"
        M --> P["🤖 Pipeline Runs Terraform & Ansible"];
        P --> Q["🌐 Provision/Update Infrastructure <br> (Kubernetes Cluster, DBs)"];
        Q --> R["🔧 Configure Servers & Install Agents"];
    end

    subgraph "4. Continuous Deployment (CD)"
        R --> V["🚀 Deploy to Staging Environment"];
        V --> W["🕹 Run Automated End-to-End Tests"];
        W -- "Fails" --> K;
        W -- "Passes" --> X{"gate:Manual QA Approval?"};
        X -- "No" --> K;
        X -- "Yes" --> Y["✅ Promote Build for Production"];
        Y --> Z["📄 Update Kubernetes Manifests"];
        Z --> AA["🚢 Pipeline executes kubectl apply"];
        AA --> BB["🔄 Kubernetes Initiates Rolling Update"];
        BB --> CC["✨ New Version is Live in Production!"];
    end

    subgraph "5. Operations & Monitoring"
        CC --> DD["📈 Collect Metrics & Logs <br> (Prometheus, ELK Stack)"];
        DD --> EE["📊 Analyze Dashboards & Logs"];
        EE --> FF{"Detect Anomaly or Issue?"};
        FF -- "No" --> EE;
        FF -- "Yes" --> GG["🚨 Send Alert Notification <br> (e.g., Slack, PagerDuty)"];
    end

    subgraph "Feedback Loop"
        GG --> A;
    end
'''
