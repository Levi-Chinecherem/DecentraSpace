digraph DecentraSpaceBackend {
    rankdir=LR;
    node [shape=rectangle, style=filled, color=lightblue];

    // Core Modules
    Auth [label="User Authentication\n- Web3 Wallet Sign-In\n- Account Tier Management"];
    GitHub [label="GitHub Integration\n- Account Linking\n- Continuous Deployment"];
    Billing [label="Billing & Credits\n- Pay-as-you-go Billing\n- Credit Management"];
    Storage [label="Decentralized Storage\n- IPFS & Arweave\n- File Management"];
    Domain [label="Domain Management\n- Purchase & Renewal\n- Decentralized DNS"];
    Hosting [label="Site Hosting\n- Static & Dynamic\n- Uptime Monitoring"];
    Blockchain [label="Blockchain Integration\n- Credit Management\n- Domain Ownership"];
    Analytics [label="Analytics\n- Site Performance\n- Credit Usage"];

    // User Flow
    User [label="User", shape=oval, style=filled, color=lightgray];
    Frontend [label="Frontend (Web/Mobile)\n- UI Only\n- API Interaction", shape=ellipse, color=lightgray];
    Admin [label="Admin", shape=oval, style=filled, color=lightgray];

    // Relationships
    User -> Frontend;
    Frontend -> Auth [label="Login / Authentication"];
    Frontend -> GitHub [label="GitHub Account Management"];
    Frontend -> Billing [label="Check Balance\nDeduct Credits"];
    Frontend -> Storage [label="Upload Files\nManage Folders"];
    Frontend -> Domain [label="Purchase / Link Domain"];
    Frontend -> Hosting [label="Deploy Site\nMonitor Status"];
    Frontend -> Blockchain [label="Manage Credits"];
    Frontend -> Analytics [label="Fetch Site Analytics"];

    // Admin Flow
    Admin -> Auth [label="Admin Management"];
    Admin -> Billing [label="Credit Policy Management"];
    Admin -> Domain [label="Domain Policy\nExpiration Control"];
    Admin -> Hosting [label="Site Expiration\nAdjustments"];
    Admin -> Analytics [label="System Health Metrics"];

    // Detailed Inter-Module Connections
    Auth -> Billing [label="Verify Tier for Limits"];
    Auth -> GitHub [label="Limit Linked Accounts"];
    Auth -> Blockchain [label="Wallet Verification"];
    Billing -> Hosting [label="Deduct Credits"];
    Billing -> Storage [label="Deduct Credits"];
    Billing -> Domain [label="Deduct Credits"];
    Billing -> Blockchain [label="Manage Credit Contracts"];
    Blockchain -> Billing [label="Notify Credit Events"];
    GitHub -> Hosting [label="Trigger Deployments"];
    GitHub -> Analytics [label="Track Deployment Status"];
    Storage -> Analytics [label="Monitor Usage"];
    Domain -> Blockchain [label="Verify Ownership"];
    Hosting -> Analytics [label="Track Uptime\nMonitor Performance"];
    Blockchain -> Analytics [label="Notify Ownership Changes"];

    // Module Descriptions
    subgraph cluster_Auth {
        label = "User Management & Authentication";
        Auth;
    }

    subgraph cluster_GitHub {
        label = "GitHub Integration";
        GitHub;
    }

    subgraph cluster_Billing {
        label = "Billing & Credits System";
        Billing;
    }

    subgraph cluster_Storage {
        label = "Decentralized Storage";
        Storage;
    }

    subgraph cluster_Domain {
        label = "Domain Management";
        Domain;
    }

    subgraph cluster_Hosting {
        label = "Hosting & Deployment";
        Hosting;
    }

    subgraph cluster_Blockchain {
        label = "Blockchain Integration";
        Blockchain;
    }

    subgraph cluster_Analytics {
        label = "Analytics & Monitoring";
        Analytics;
    }
}
