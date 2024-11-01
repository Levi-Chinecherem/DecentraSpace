digraph DecentraSpaceArchitecture {
    rankdir=LR; // Left to Right layout

    // Define primary nodes
    User[shape=ellipse, label="User (Free/Paid)"];
    Browser[shape=box, label="User's Browser"];
    Wallet[shape=ellipse, label="Web3 Wallet\n(Anon Auth)"];
    Frontend[shape=box, label="Frontend\n(React, Next.js)"];
    Backend[shape=box, label="Backend (Django API)"];
    SmartContract[shape=ellipse, label="Smart Contract\n(Blockchain)"];
    Admin[shape=ellipse, label="Admin Panel"];

    // Storage and Data Management
    IPFS[shape=parallelogram, label="IPFS\n(Static Assets)"];
    Arweave[shape=parallelogram, label="Arweave\n(Permanent Storage)"];
    Database[shape=parallelogram, label="Decentralized Database"];
    StorageService[shape=parallelogram, label="On-Demand File Storage"];
    DNS[shape=parallelogram, label="Decentralized DNS\n(e.g., ENS, HNS)"];

    // GitHub Integration
    GitHub[shape=ellipse, label="GitHub Integration"];
    Analytics[shape=parallelogram, label="Analytics Service\n(Site Performance)"];
    
    // Define connections and interactions
    subgraph cluster0 {
        label="User Interface";
        Browser -> Wallet [label="Web3 Authentication"];
        Wallet -> Frontend [label="Authenticate"];
        Browser -> Frontend [label="Interact with UI"];
    }

    subgraph cluster1 {
        label="Frontend";
        Frontend -> Backend [label="REST API Calls"];
        Frontend -> GitHub [label="GitHub Deployments"];
        Frontend -> Analytics [label="Performance Tracking"];
    }

    subgraph cluster2 {
        label="Backend";
        Backend -> SmartContract [label="Execute Contract\n(Tier Mgmt, Billing)"];
        Backend -> Database [label="DB Operations\n(Usage Tracking, Tier Info)"];
        Backend -> DNS [label="DNS Record Mgmt\n(Link Domains)"];
        Backend -> IPFS [label="Upload/Fetch Static Assets"];
        Backend -> Arweave [label="Upload/Fetch Permanent Data"];
        Backend -> StorageService [label="Manage File Storage"];
    }

    subgraph cluster3 {
        label="Smart Contract & Blockchain";
        SmartContract -> Wallet [label="Credit Management\nTransaction Handling"];
        SmartContract -> Backend [label="Event Trigger\n(Credit Status)"];
        SmartContract -> DNS [label="Domain Ownership\nVerification"];
        Admin -> SmartContract [label="Update Expiry Duration"];
    }

    subgraph cluster4 {
        label="Hosting Services";
        IPFS -> Frontend [label="Deliver Content\n(CDN Access)"];
        Arweave -> Frontend [label="Deliver Content\n(Permanent Links)"];
        DNS -> Frontend [label="Domain Linking"];
        StorageService -> Frontend [label="On-Demand File\nAccess/Download"];
        Database -> Frontend [label="DB Queries"];
    }

    // User Actions
    User -> Browser [label="Access Dashboard"];
    User -> Wallet [label="Anon Auth"];
    User -> Admin [label="Admin Panel Access"];
    Admin -> Backend [label="Adjust Free Tier Limit"];

    // Backend Services and Tier Management
    Backend -> Wallet [label="Charge Credits"];
    Backend -> Admin [label="Admin Actions\n(Update Expiry)"];
    Backend -> GitHub [label="Integrate Deployment\nfrom GitHub"];

    // Node for Credit System
    CreditSystem[shape=ellipse, label="Credit Management"];
    Backend -> CreditSystem [label="Credit Deduction\nand Top-Up"];
    User -> CreditSystem [label="Purchase Credits"];

    // Notes
    note1 [shape=note, label="Site Expiry\nFree Tier: 6 months"];
    note2 [shape=note, label="Upgrade to Paid Tier\nRequires Credits"];
    note3 [shape=note, label="Dynamic 'Pay-as-you-go'\nBilling Mechanism"];

    Backend -> note1;
    CreditSystem -> note2;
    Backend -> note3;
}
